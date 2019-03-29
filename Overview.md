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
