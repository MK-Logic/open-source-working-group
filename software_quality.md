# Software Quality in Z-Wave Alliance Open Source Project

Want to contribute? Great! To ensure that the Z-Wave source has a high quality and can be used for mass market 
products, a number of quality ensurance steps must be taken when contributing code.

## Unit test

The Z-Wave source contains a set of unit tests based on [unity](https://github.com/ThrowTheSwitch/Unity) and [CMock](https://github.com/ThrowTheSwitch/CMock). The unit tests must be run and **pass** on all source code changes in the Z-Wave stack repository. If a change in the Z-Wave code breaks a unit test, the code or the test must be fixed so the test passes. It is not allowed to disable any unit tests to get a test run to pass, no matter what the failure is caused by.

When adding code to the Z-Wave source, new unit tests must be added to ensure that the line coverage of new code is at least 80%, if this is not possible it must be clearly stated in the pull request and a Community Leader must approve the lover test coverage. It is allowed to combine line coverage for unit test and system level test to achieve the 80% line coverage.

## System Level Test

The Z-Wave source code contains a number of system level test cases that ensures that the Z-Wave implementation is in accordance with the latest Z-Wave MAC and Network layer specifications. All system level tests must be run and **pass** on all source code changes in the Z-Wave stack repository. If a change in the Z-Wave code breaks a system level test, the code or the test must be fixed so the test passes. It is not allowed to disable any system level tests to get a test run to pass, no matter what the failure is caused by. An expection to this rule is if the test failure is identified as beeing a bug in the Z-Wave specifications. In this case a system level test can be temporarily disabled until the specification has been changed and the test has been updated to reflect the change.

### MAC level tests

The MAC layer tests are based on:

[Z-Wave MAC Layer Test specification](https://sdomembers.z-wavealliance.org/wg/Members/document/901)

and 

[Z-Wave Long Range MAC Layer Test Specification](https://sdomembers.z-wavealliance.org/wg/Members/document/898)

Not all test cases mentioned in the MAC level tests can be implemented as system level tests, some tests requires a correct PHY layer implementation and can therefore not be implemented in the Z-Wave source project on Linux. The OSWG group will maintain a list of MAC level tests that are not implemented as 
automated MAC level tests so stack developers knows what MAC tests they need to pay extra attention to when developing the PHY layer for a specific hardware platform.

MAC layer test cases for the Z-Wave source can be found [here](https://github.com/Z-Wave-Alliance/z-wave-stack/tree/main/test/MAC)

### Network layer tests

The Network layer tests are based on:

[Z-Wave Nwtwork Layer Test specification](https://sdomembers.z-wavealliance.org/wg/Members/document/1007)

and 

[Z-Wave Long Range Network Layer Test Specification](https://sdomembers.z-wavealliance.org/wg/Members/document/899)

All test cases in the Network layer test specifications should be implemented as system level test in the 
Z-Wave stack source code project.

Network layer test cases for the Z-Wave source can be found [here](https://github.com/Z-Wave-Alliance/z-wave-stack/tree/main/test/NWK)

## Bugs

When fixing a bug it is important that the bug fix is simple and does not touch code that is not related to fixing the bug. To maintain the quality of the code when fixing bugs, it is important that tests are also implemented to ensure that the bug is fixed. Best practise is to first implement a unit or system level test that can reproduce the problem and then change the code so the test passes.

Some bugs are hard to test automatically in the Z-Wave source project, if they are e.g. related to timing or specific behavior of the physical layer. In that case a bug can be fixed without implementing a test.

## New Features

New features must be in accordance with the Z-Wave specifications and it is required that all new features are covered by at 
least 80% line coverage in test. Best practise is to use unit test to test the logical functionality of the new feature and to use system level test to test that the new feature works together with the rest of the protocol stack or applications.

## Release Requirements

When making a release of the Z-Wave source it is important that a high quality of the release is ensured. To maintain the high quality it is mandatory to go through the following steps:

1. Lock the main branch in github to ensure that no code is merged during the release process.
2. Make sure that all Pull Requests (PR) that are going into the release has been reviewed and merged and are done according to the contributon guidelines.
3. Make sure that the CI runs with no errors
    1. Build
    2. Link
    3. Unit test
    4. System test
    5. Code Style Analysis
4. (Optional) Submit the release for test at a Z-Wave test house
5. Get approval from at least one silicon or stack vendor that has run the release through their internal test
6. Tag the release in github
7. Make a release note with highlights of changes since last release
