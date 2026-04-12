# Smart Monitor Playwright Project Practices

## Observed project conventions

These conventions were derived from the Smart Monitor Playwright repository and developer review notes.

## Auth and session reuse

- The project Playwright config uses `storageState` with `.playwright/.auth/user.json`.
- Auth is created in `tests/auth.setup.ts`.
- This means repeated UI login inside every test is usually the wrong default.
- Prefer setup-based auth first.
- If smoke or environment validation still needs UI-login fallback, reuse existing helper functions instead of duplicating auth flows.

## Suite structure

- Existing suites often use `test.describe.configure({ mode: 'serial' })`.
- Existing suites often create a suite-level `Page` in `beforeAll`.
- The suite then reuses that page across tests instead of destructuring `{ page }` in every test.
- This is effectively a singleton page pattern at suite level.

## Browser support

- The Playwright config defines Chromium, Firefox, and WebKit projects.
- New tests must avoid browser-specific assumptions unless clearly required.
- Keyboard shortcuts should use cross-platform forms such as `ControlOrMeta`.
- Avoid selectors or interactions that are known to behave inconsistently across engines unless guarded and documented.

## Selector policy

- The configured test id attribute is `data-test-subj`.
- Prefer `page.getByTestId(...)`.
- Avoid localized selectors based on Russian labels, headings, placeholders, or button text when a test id exists or should exist.
- Avoid CSS-only locators when the same target has a stable test id.
- If a stable test id is missing, prefer requesting or documenting it rather than normalizing a weak selector as permanent style.

## Legacy patterns observed in current tests

Some existing repository tests still contain patterns that should not become the default standard:

- `getByText(...)` for localized UI labels;
- `getByRole(..., { name: '...' })` tied to Russian wording;
- placeholder-based login selectors;
- CSS locators such as `.ouiFieldSearch`, `.ouiBasicTable`, or toast class selectors when a stable test id would be better;
- suite implementations that mix good test-id usage with temporary fallback selectors.

Treat these as transitional patterns unless the repository clearly lacks a better selector.
New generated tests should prefer the stronger project-standard path.

## Shared helpers

Existing helper patterns already include:
- page error logging;
- dynamic app path opening with install-prefix support;
- loader wait;
- login guard;
- fatal application error guard.

Prefer reusing these helpers over writing local one-off replacements.

## Assertions

- Core business outcomes should use strong assertions.
- Secondary or supporting checks may use `expect.soft`.
- Expect messages should be added when the failure would otherwise be ambiguous.
- Negative validation checks should remain readable and intentional.

## Naming and metadata

- Add the `AT` prefix to created entities where that convention is required.
- Include `SMTEST` case identifiers in test or suite names when available from the source testcase.
- Preserve priority, depth, and other project markers from the testcase or repository conventions.

## Test readability

- Use `test.step` for the main phases of the scenario.
- Keep comments only around important technical choices, unstable areas, or intentional compromises.
- Avoid long narrative comments that restate obvious code.

## Independence

- Each test should remain independently understandable and operationally safe.
- Shared page reuse in a serial suite is acceptable only when the suite still manages state intentionally and does not create hidden coupling.

## Cross-module observations

Across `job-scheduler`, `sigma-rules`, and `macros`:
- suite-level shared page usage is common;
- page error logging is common;
- `data-test-subj` usage is already strong in many flows;
- some older specs still rely on localized text and CSS selectors;
- cleanup logic may appear in `afterAll` for imported or created data.

Use the strong patterns as defaults.
Treat the weaker patterns as migration debt, not as the target style.
