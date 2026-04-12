# Smart Monitor Test Case Authoring Regulation

## Purpose

This document fixes the working regulation for writing manual test cases and choosing automation candidates for Smart Monitor.
The regulation is mandatory before creating new manual cases or proposing new autotests.

## Mandatory workflow before writing new cases

1. First review the current manual cases in the team knowledge base.
2. Then review the current autotests in the Smart Monitor Playwright repository.
3. Then review durable project context:
   - current handoff notes;
   - current QA project memory;
   - smoke matrices and current smoke plans;
   - delivery planning notes;
   - automation backlog notes.
4. Only after the review is complete, design a new case or improve an existing one.
5. Do not duplicate an existing manual case or an already sufficient autotest-backed scenario without a clear gap.

## Core rules

1. All test cases must be written in Russian.
2. One test case must cover one check and one goal.
3. Every test case must be reproducible by a person without extra explanation.
4. Each step must describe one user action only.
5. Each step must explicitly state navigation, clicks, text entry, selections, and modal interactions when they happen.
6. Expected results must be observable and verifiable.
7. Avoid vague wording like `проверить, что все работает`, `данные корректны`, `все успешно открылось`, `интерфейс работает штатно` without a visible condition.
8. If the product behavior is not confirmed by sources, mark it as `требует уточнения` or `допущение` instead of inventing details.
9. Use existing Smart Monitor terminology from current cases, autotests, and UI labels.
10. Design every case so it can later be moved into Playwright or another automation layer with minimal rewriting.

## Required case structure

For repository consistency, YAML keys may remain in English, but all human-readable values must be in Russian unless the UI uses another language.

Required fields:
- `id`
- `title`
- `product`
- `module_path`
- `component`
- `priority`
- `type`
- `status`
- `description`
- `preconditions`
- `test_data`
- `steps_table`
- `postconditions`
- `automation`

Recommended additional fields when useful:
- `tags`
- `links`
- `notes`
- `known_limitations`

## Step block standard

The step block must be formatted only as a table with these columns:
- `No.`
- `Шаг`
- `Данные`
- `Ожидаемый результат`

In YAML this should be stored as `steps_table` with one row per action.

Example row structure:

```yaml
steps_table:
  - number: 1
    step: Открыть раздел Планировщик задач в левом меню.
    data: Не требуется.
    expected_result: Открывается страница списка задач Планировщика задач.
```

## Writing rules for steps and expected results

- Use imperative user actions: `Открыть`, `Нажать`, `Ввести`, `Выбрать`, `Закрыть`.
- Do not combine several actions in one row.
- Do not hide transitions between pages or sections.
- If a modal opens, opening and closing it are separate steps.
- If a value is entered into a field, name the field and the value source.
- If a selection is made from a dropdown, name the dropdown and the selected value.
- Each expected result must refer to visible UI state, URL change, toast, row in table, field value, button state, modal state, or another observable signal.

## Automation-oriented rules

- Every case must include an `automation` block.
- The block must answer:
  - whether the case is a good automation candidate;
  - the preferred automation layer: `unit`, `api`, `integration`, `ui-e2e`;
  - whether an existing Playwright spec already covers the scenario fully or partially.
- Prefer `ui-e2e` only for user-visible flows, routing, forms, shell availability, and role-sensitive checks.
- If a similar autotest already exists, link it instead of proposing a duplicate candidate.
- If no autotest exists, propose one candidate file name using the current repo naming style.

## Naming and structure conventions

### Manual case IDs

- Keep short module prefixes already used in the knowledge base, for example: `JS`, `SET`.
- For new modules, use stable readable prefixes, for example: `DASH`, `SIG`, `NB`, `MAC`, `RSM`.

### Manual case file names

- Format: `<ID>-<short-kebab-slug>.yaml`
- Example: `DASH-002-open-and-cancel-create-modal.yaml`

### Autotest file names

- Follow the existing repo style: `<module>-<scenario>.spec.ts`
- Examples:
  - `dashboard-list-read.spec.ts`
  - `sigma-rules-smoke.spec.ts`
  - `job-scheduler-user-story-full-flow.spec.ts`

## Definition of ready for a new test case

A test case is ready only if:
1. It is based on reviewed current context.
2. It has one goal.
3. It has all mandatory fields.
4. Its steps are in table form.
5. Every step contains one user action.
6. Every expected result is directly checkable.
7. It does not duplicate an existing case without reason.
8. It is linked to existing automation or has a clear automation candidate.
9. All unsupported assumptions are explicitly marked.

## Current quality gaps to avoid

The current repository already shows some patterns that should not be repeated in new cases:
- overly broad interface checks bundled into one case;
- several user goals inside one scenario;
- steps that hide navigation or combine many actions;
- expected results phrased too generally;
- draft cases without clear automation mapping.

## Minimal YAML skeleton

```yaml
id: MOD-001
title: Краткое название одной проверки
product: smart-monitor
module_path:
  - smart-monitor
  - section
  - module
component: list-page
priority: P1
type: smoke
status: draft
description: Краткое описание одной проверяемой цели.
preconditions:
  - Пользователь авторизован в Smart Monitor.
test_data:
  query: example
steps_table:
  - number: 1
    step: Открыть нужный раздел через левое меню.
    data: Не требуется.
    expected_result: Открывается целевая страница без ошибки.
postconditions:
  - Изменения не сохранены.
automation:
  candidate: true
  level: ui-e2e
  related_playwright:
    - tests/example.spec.ts
```
