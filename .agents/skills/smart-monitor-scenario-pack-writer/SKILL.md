---
name: smart-monitor-scenario-pack-writer
description: Use when the task is to write or normalize a Smart Monitor manual testcase, scenario pack, or regulated QA scenario from requirements, examples, or existing manual cases. Best for converting rough flows into one-goal, reviewable testcase artifacts.
---

# Smart Monitor Scenario Pack Writer

Write stable manual testcase artifacts for Smart Monitor.

## Use this skill when

- the user needs a manual testcase or scenario pack;
- a rough flow must be converted into a regulated testcase;
- an existing testcase must be normalized to one approved format;
- automation planning needs a clean manual source artifact first.

## Output contract

Produce one scenario pack per goal.

Each output should contain:
- title;
- goal;
- preconditions;
- test data;
- steps;
- expected results;
- assumptions or unknowns;
- automation-candidate note.

## Hard rules

- One scenario equals one goal.
- One step equals one user action.
- Expected results must be observable.
- Mark unknown behavior explicitly.
- Do not generate Playwright code.
- Do not merge several user goals into one testcase.

## Workflow

1. Read the current testcase standard first.
   Path: `skill-design-inputs/manual-testcase-regulation/REGULATION.md`
2. If good manual examples exist, align structure and depth to them.
   Path: `skill-design-inputs/manual-testcases-good/`
3. Write the smallest complete testcase that still supports later automation.
4. Call out missing information instead of inventing hidden behavior.

## Style rules

- Prefer compact wording over prose.
- Use domain terms consistently.
- Keep the testcase reviewable by a human QA engineer.
- Prefer stable field names across outputs.

## If artifacts are still incomplete

If the regulation or examples are missing, stay conservative:
- keep the format simple;
- make assumptions explicit;
- avoid domain-specific wording that is not supported by inputs.
