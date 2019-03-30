# Types of Tests
## Unit Tests
Tests a specific unit of functionality such as each methods in a class or plain functions. You focus only on that piece of code without depending on any other objects. Any dependencies smells like it could be redesigned to avoid dependency. If it is an essential dependency it could be replaced with a test double.

## Integration Tests
Though Unit Tests makes sure that each objects do work fine to meet their requirements, it may end in chaos while interacting with outside objects. Integration Tests rule out this issue by testing a specific interaction flow between an object and another object such as our piece of code interacting with DB, Network, File System etc or even interactions between two different class objects.

For example on Integration Tests, let's assume how Integration Tests of API would look like:

1. Start a server and listen to HTTP requests
2. Grab a request and authenticate the user
3. Validate a request
4. Connect to DB and pull required data
5. Convert to JSON
6. Send back

Here, the complete workflow of an API request is tested through integration tests which covers the user request handling module, authentication module, DB interaction, and JSON conversion of response.

If a code that has some business logic prior to interacting with DB, the business logic units are tested using Unit Tests, and the interaction with DB is tested using Integration Tests.

## End To End Tests (E2E Tests - Acceptance Tests, Functional Tests, UI Tests)

Tests on the use case scenarios. In this phase you test application entirely like how a user would interact with a website through a browser. This involves DOM parsing and UI tests.

For example on E2E, let's assume how E2E of mail application would look like:

1. Start a webserver to launch your mail application
2. Launch a browser
3. Log into a mail account
4. Open Inbox
5. Open a particular mail
6. Compose a reply to that mail
7. Send mail
8. etc
9. Log out of mail account

# Unit Tests
## How To write Unit Tests to drive TDD

In TDD, unit tests are driven through 3 stages in the following strategy.

**RED:** Just specify one of small requirement using a unit test which of course fails because the code is not yet written.

**GREEN:** Write the code just enough to make the above unit test as green. You may do hard coding or at worst do coding just enough with the aim to pass the above test. The prime goal in this step is to write code in smallest possible time not more than a few minutes.

**REFACTOR:** Then refactor codes to improve quality of codes and and clean them to remove hard coding.
This ensures to make __clean code that works__. _"Clean code"_ is ensured by _refactor stage_. And, _"that works"_ is ensured by _Red to Green_ stage

Generally, you would write unit tests on a class's public interface. Hence, that interface would evolve into an _easy to use_ one rather than an _easy to write_ counter intuitive interface that you might develop otherwise.

Every few minutes, unit tests helps to provide a proven code, that has been tested, designed and coded.

## Rules of Unit Tests

- Each test should be independent so that all the tests can be run simultaneously.
- Any dependencies for a particular test must be implemented using a _mock_ or _stub_. Do not depend on another test result.
- Each test should represent a unit of behavior.
- What we expect from a piece of code must be described through unit tests. So essentially we are writing specifications of project through each tests.
- In a way it is documenting behavior of a project through each test.
- Here you have to imagine at first what am I expected as result from executing a piece of code before even starting to write any code.
- As a result you will write only for the necessary scope of project. You don't end up writing any code unnecessarily. This approach is called **YAGNI - You Aren't Gonna Need It**.
- Unit tests should be fast in execution. By fast we can expect to see a 100 unit tests should be executed within 1 sec

## When NOT to depend on Unit Tests ?

Unit tests should strictly focus on the unit of functionality you are writing, which means there should be:
- No touch on file system
- No talk with DB
- No network traversal
- No configuration changes needed for a particular test
- The above kinds of tests are called integration tests.
- You don't need to test private methods. If there is need to test a private method, that indicates need for refactoring code for public interface.
- You don't need to test code which doesn't have any logic. For example, getters, setters, a method which simply invokes another method.

## Features offered by a Unit Test library

### A. Verification

#### 1. State verification
Checks if the SUT (System Under Test) has arrived at expected state during test execution.

#### 2. Behavior verification
Checks if a particular method is invoked during test execution.

### B. Test Double

#### 1. Stub 
If your unit test relies on another method which has complex logic but eventually returns a true or false, or a specific data, then you can substitute such complex methods with a shortcut function returning that expected return value. This approach in unit testing is called stubbing.

#### 2. Spy 
Spy is wrapper on an object to primarily serve two purposes. One is to identify how an object is being used, and second is to avoid alteration of a function behavior. When an object is invoked via spy it will monitor the parameters being passed, count of invocation etc.

#### 3. Mock 
Mock is like a spy + stub where it returns a pre-programmed response like a stub in addition to monitoring the invocation like spy. Mock is used when you want to track the behavior of invocation while providing hard coded response.

#### 4. Fake
If you need data to be retrieved from DB in order to execute test on a piece of code, then unit test doesn't need to bother about the DB dependency. In this case you could set a hard coded data to avoid executing complex DB data retrieval methods, and also you don't need to worry about DB connection failures. To ease with testing you could provide Fake object (for eg: which may be a list of employees), or an in-memory DB instead of real DB.

#### 5. Dummy
Dummy data passed to methods.

# Test Based Development Techniques

## Test Driven Development (TDD)

In TDD, development is done based on Unit Tests. Here, you would write a piece of code only to turn the _RED unit tests to GREEN_. Every bit of code is driven by unit tests.

## Behavior Driven Development (BDD)

BDD is a strategy build on top of TDD. In BDD, we focus on the user stories to build a software. 

- Write Unit Tests for a Story
- Code that story following TDD
- So here we code to the behavior represented in user story. BDD is TDD with strict focus on stories. Business people, Managers, Developers, Testers - all are looking into same set of stories.
- Stories are prioritized during sprint, and
- Each story reflects on the business value it provides. There is standard template for user story as presented below.
- There are test frameworks which works based on user stories based implementation such as _Cucumber_.

# User Story Template

**Title:** One line summary

**Narrative:** As a *role*, I want this *feature*, So as to get this *benefit*

**Acceptance criteria:** Specify scenarios which stakeholders do care about or a tester need to look into.

# Contrast BDD over TDD

_TDD_ essentially is locking us into the implementation style. But, _BDD_ only cares about the behavior, not your implementation style. Therefore, _BDD_ allows you to refactor a lot without causing troubles or test failures. But, _TDD_ would fail if you change implementation because _TDD_ is executed on each unit of code written.

Take for example your code has a logic to sort numbers in increasing order.

_TDD approach_ : Let's say you implemented sorting using Quick sort algorithm, and your unit tests verify that specific algorithm. If we happened to change the algorithm to Bubble sort for some reason, then your unit test would fail because it is expecting Quick sort algorithm.

_BDD approach_ : Let's say you implemented sorting using Quick sort algorithm, and your BDD is only verifying the outcome, not your specific algorithm. If we happened to change the algorithm to Bubble sort for some reason, then your BDD will not fail because it is expecting only the outcome or behavior to be sorted list of numbers no matter which algorithm is used.
