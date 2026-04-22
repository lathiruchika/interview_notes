# BDD Tags in Behave (Complete Notes)

## Overview
Tags in Behave are used to organize, filter, and control test execution.

They can be applied to:
- Features
- Scenarios
- Scenario Outlines

---

## 1. Adding Tags

### Scenario Level
```
@smoke
Scenario: Successful login
```

### Scenario Outline
```
@regression @login
Scenario Outline: Login with multiple credentials
```

### Feature Level
```
@login_feature
Feature: Login functionality
```

---

## 2. Tag Inheritance

- Feature-level tags apply to all scenarios inside it

---

## 3. Running Tests Using Tags

### Run Smoke Tests
```
behave --tags=smoke
```

### Run Regression Tests
```
behave --tags=regression
```

### AND Condition
```
behave --tags="smoke and login"
```

### OR Condition
```
behave --tags="smoke or regression"
```

### Exclude Tag
```
behave --tags="not slow"
```

---

## 4. Example Feature File

```
@login_feature

Feature: Login functionality

  @smoke
  Scenario: Successful login
    Given user is on login page

  @regression @negative
  Scenario Outline: Login with multiple credentials
    When user enters username "<username>" and password "<password>"

  Examples:
    | username | password |
    | user1    | pass1    |
    | user2    | pass2    |
```

---

## 5. Hooks with Tags

### environment.py

```python
def before_scenario(context, scenario):
    if "smoke" in scenario.tags:
        print("Running smoke setup")

    if "regression" in scenario.tags:
        print("Running regression setup")
```

---

## 6. Real Use Cases

- Run only smoke tests in CI
- Run regression suite nightly
- Skip slow tests
- Run tests for specific environments (qa, prod)

---

## 7. Tagging Strategy (Best Practice)

| Tag Type | Example |
|----------|--------|
| Test Type | @smoke, @regression |
| Layer | @ui, @api |
| Nature | @positive, @negative |
| Environment | @qa, @prod |

---

## 8. Common Mistakes

- Too many random tags
- No naming convention
- Mixing business and technical tags

---

## 9. Interview Answer

Tags are used in BDD to group and filter test scenarios, enabling selective execution and dynamic behavior when combined with hooks.

---

## Generated On
2026-04-02 13:00:51.607258