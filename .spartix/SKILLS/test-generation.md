# Skill: Test Generation

## Name
test-generation

## Version
1.0.0

## Description
Generate test cases, test suites, and test data for code and features. Covers unit tests, integration tests, end-to-end tests, performance tests, and security tests with appropriate assertions and coverage targets.

## Parameters
- **test_type**: Type of tests to generate (unit, integration, e2e, performance, security)
- **framework**: Testing framework (Jest, Pytest, Cypress, Playwright, JUnit)
- **coverage_target**: Minimum code coverage percentage required
- **test_data_strategy**: How test data should be generated (factories, fixtures, mocks, synthetic)

## Outputs
- Test files with complete test cases and assertions
- Test data factories or fixtures
- Coverage report showing achieved coverage against target
- Test execution instructions

## Prerequisites
- Source code to test must be available from predecessor tasks
- Testing framework must be specified in the task packet
- Coverage targets must be defined in the acceptance criteria

## Approved Categories
- 10_QA_TESTING_AND_VALIDATION
- 04_FRONTEND_WEB_SPECIALISTS
- 05_BACKEND_AND_API_SPECIALISTS

## Usage Rules
- Tests must be deterministic and repeatable — no flaky tests
- Test data must not contain real PII or sensitive information
- All test cases must include clear descriptions of what they validate
