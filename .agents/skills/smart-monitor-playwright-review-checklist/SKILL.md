---
name: smart-monitor-playwright-review-checklist
description: Use when reviewing Smart Monitor Playwright tests or validating generated test code against the team's actual automation practices. Best for catching weak selectors, duplicated code, bad auth patterns, missing metadata, and multi-browser risks before merge.
---

# Smart Monitor Playwright Review Checklist

Review Smart Monitor Playwright code against the team's actual conventions.

## Use this skill when

- a new Playwright test has been generated;
- an existing Playwright test has been repaired;
- the task is code review or pre-merge QA review for Playwright specs.

## Read first

- `../smart-monitor-playwright-automation-writer/references/project-practices.md`
- `../smart-monitor-playwright-automation-writer/references/review-checklist.md`

## Output style

Lead with findings.

For each finding, state:
- what is wrong;
- why it matters;
- what pattern should be used instead.

## Hard rules

- Treat weak selectors as real findings, not style nits.
- Treat repeated UI login as a performance and stability finding when project auth setup already exists.
- Treat missing `test.step`, missing skip reasons, and missing useful expect messages as quality findings when they reduce maintainability or diagnosis quality.
- Call out missing multi-browser awareness when the code is likely Chromium-only.
- Call out missing helper reuse when the same behavior already exists in project helpers.

## Focus areas

- selector stability;
- helper reuse;
- auth strategy;
- singleton page or suite lifecycle consistency;
- assertion clarity;
- `expect.soft` usage;
- tags and testcase metadata;
- `AT` naming for created entities;
- `SMTEST` naming linkage;
- test independence;
- meaningful comments only where needed;
- browser-project safety.
