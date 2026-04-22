# BDD Background (Detailed Notes)

## Overview
Background in BDD is used to define common steps that are executed before every scenario in a feature file.

It helps reduce duplication and improves readability.

---

## 1. What is Background?

Background is a section in a feature file that contains steps executed before each scenario.

---

## 2. Syntax

```
Feature: Login functionality

  Background:
    Given user is on login page

  Scenario: Successful login
    When user enters username "user1" and password "pass1"
    Then user should see "dashboard"
```

---

## 3. Execution Flow

```
Background runs
   ↓
Scenario 1 runs
   ↓
Background runs again
   ↓
Scenario 2 runs
```

---

## 4. Example

```
Feature: Login functionality

  Background:
    Given user is on login page

  Scenario: Successful login
    When user enters username "valid_user" and password "valid_pass"
    And clicks login button
    Then user should see "dashboard"

  Scenario: Invalid login
    When user enters username "invalid_user" and password "wrong_pass"
    And clicks login button
    Then user should see "error"
```

---

## 5. Step Definitions

Background steps reuse the same step definitions as scenarios.

```python
@given("user is on login page")
def step_open_login(context):
    context.login_page.open()
```

---

## 6. Rules

- Only one Background per feature
- Runs before every scenario
- Should contain common steps only

---

## 7. Background vs Hooks

| Background | Hooks |
|-----------|------|
| Written in feature file | Written in Python |
| Business readable | Technical |
| Used for test flow | Used for setup/teardown |

---

## 8. Best Practices

- Keep Background short and simple
- Use for common steps only
- Avoid complex logic
- Do not include assertions

---

## 9. Common Mistakes

- Adding too many steps in Background
- Using Background for scenario-specific logic
- Writing duplicate steps

---

## 10. Interview Answer

Background in BDD is used to define common preconditions that run before every scenario, improving readability and reducing duplication.

---

## Generated On
2026-04-03 03:24:38.942526