# Smart Monitor Playwright Review Checklist

Use this as the final pass before accepting a new or updated Playwright test.

## Required checks

- Selectors are correct and primarily use test ids.
- The test does not depend on localization for its main locators.
- Shared helpers or utility functions are reused instead of duplicating code.
- Assertions are clear and meaningful.
- Secondary checks use `expect.soft` only where appropriate.
- Priority, depth, and other required testcase markers are preserved.
- Created entities use the `AT` prefix where required.
- The test or suite naming includes the `SMTEST` identifier when available.
- The test is not implicitly dependent on another test.
- Important implementation choices are documented briefly when needed.
- Skip reasons are explicit.
- Expect failure messages are explicit when ambiguity would hurt diagnosis.
- Major scenario phases are wrapped in `test.step`.

## Additional checks

- The auth strategy matches the project setup and does not repeat expensive login unnecessarily.
- The suite is safe for Chromium, Firefox, and WebKit.
- No Russian-heading or localized-text locator remains when a test-id-based selector is possible.
- If coverage instrumentation is required by the project flow, the test change does not break that flow and follows repository guidance.
