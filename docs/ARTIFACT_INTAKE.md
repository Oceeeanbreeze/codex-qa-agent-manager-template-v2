# Artifact Intake

## Goal

Make skill-design inputs easy to prepare, review, and reuse.

## Best way to provide materials

Use the repository itself as the intake area.

Put the first materials into:
- `skill-design-inputs/manual-testcase-regulation/`
- `skill-design-inputs/manual-testcases-good/`
- `skill-design-inputs/playwright-good/`
- `skill-design-inputs/playwright-bad/`
- `skill-design-inputs/failures/`

You can still paste small examples into chat, but repository files are better because:
- they are easier to review;
- they stay reusable for future skills;
- they reduce ambiguity during skill design;
- they give us stable inputs for later evals.

## What is required first

### Required
- manual testcase regulation or template
- 2-5 good manual testcases
- 2-5 good Playwright tests
- 2-5 bad or problematic Playwright tests
- failure examples

### Strongly preferred
- short notes about why a testcase is good
- short notes about why a Playwright test is good or bad
- real root cause for each failure example

## File format

### Manual regulation
- format: `.md`
- language: your normal working language
- one main regulation file is enough

### Good manual testcases
- format: `.md`
- one testcase per file

### Good Playwright tests
- format: `.ts`
- one test file or one focused spec fragment per file

### Bad Playwright tests
- format: `.ts`
- one file or one focused fragment per file

### Failures
- format: `.md`
- one failure per file

## Naming convention

Use simple stable names:

- `manual-testcase-regulation/REGULATION.md`
- `manual-testcases-good/CASE-01.md`
- `manual-testcases-good/CASE-02.md`
- `playwright-good/GOOD-TEST-01.ts`
- `playwright-good/GOOD-TEST-02.ts`
- `playwright-bad/BAD-TEST-01.ts`
- `playwright-bad/BAD-TEST-02.ts`
- `failures/FAILURE-01.md`
- `failures/FAILURE-02.md`

## Important safety rule

Do not place any of these into the repository:
- real secrets
- cookies
- tokens
- raw auth headers
- production-only URLs if they are sensitive
- screenshots with sensitive data
- HAR files
- raw logs that may contain credentials

If an example comes from a sensitive case, redact it first and keep only the information needed for skill design.
