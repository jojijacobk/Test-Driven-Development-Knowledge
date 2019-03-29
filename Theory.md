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

## Rules of Unit Tests

- Each test should be independent so that all the tests can be run simultaneously.
- Any dependencies for a particular test must be implemented using a _mock_ or _stub_. Do not depend on another test result.
- Each test should represent a unit of behavior.
- What we expect from a piece of code must be described through unit tests. So essentially we are writing specifications of project through each tests.
- In a way it is documenting behavior of a project through each test.
- Here you have to imagine at first what am I expected as result from executing a piece of code before even starting to write any code.
- As a result you will write only for the necessary scope of project. You don't end up writing any code unnecessarily. This approach is called **YAGNI - You Aren't Gonna Need It**.
- Unit tests should be fast in execution. By fast we can expect to see a 100 unit tests should be executed within 1 sec
