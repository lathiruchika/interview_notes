# BDD Tags & Hooks (Detailed Notes)

## Overview
This document covers:
- Tags in Behave
- Hooks in Behave
- Usage, examples, and best practices

---

# 🏷️ TAGS IN BDD

## What are Tags?
Tags are labels used to organize and control test execution.

They can be applied to:
- Feature
- Scenario
- Scenario Outline

---

## Adding Tags

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

## Tag Inheritance
- Feature-level tags apply to all scenarios inside it

---

## Running Tests Using Tags

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

## Example Feature File

```
@login_feature

Feature: Login functionality

  @smoke
  Scenario: Successful login
    Given user is on login page

  @regression @negative
  Scenario Outline: Login with multiple credentials
    When user enters username "<username>" and password "<password>"
```

---

## Tag Strategy (Best Practice)

| Tag Type | Example |
|----------|--------|
| Test Type | @smoke, @regression |
| Layer | @ui, @api |
| Nature | @positive, @negative |
| Environment | @qa, @prod |

---

## Common Mistakes

- Too many random tags
- No naming convention
- Mixing business and technical tags

---

# 🔁 HOOKS IN BDD

## What are Hooks?
Hooks are lifecycle methods that run automatically before/after test execution.

---

## Execution Flow

```
before_all
before_feature
before_scenario
before_step
STEP EXECUTION
after_step
after_scenario
after_feature
after_all
```

---

## Hook Types

### before_all
Runs once before all tests

```python
def before_all(context):
    context.playwright = sync_playwright().start()
```

---

### after_all
Runs once after all tests

```python
def after_all(context):
    context.playwright.stop()
```

---

### before_feature
Runs before each feature

```python
def before_feature(context, feature):
    print(f"Starting Feature: {feature.name}")
```

---

### after_feature
Runs after each feature

```python
def after_feature(context, feature):
    print(f"Completed Feature: {feature.name}")
```

---

### before_scenario
Runs before each scenario

```python
def before_scenario(context, scenario):
    context.browser = context.playwright.chromium.launch()
    context.page = context.browser.new_page()
```

---

### after_scenario
Runs after each scenario

```python
def after_scenario(context, scenario):
    context.browser.close()
```

---

### before_step
Runs before each step

```python
def before_step(context, step):
    print(f"Executing Step: {step.name}")
```

---

### after_step
Runs after each step

```python
def after_step(context, step):
    if step.status == "failed":
        print("Step failed")
```

---

## Hooks with Tags

```python
def before_scenario(context, scenario):
    if "smoke" in scenario.tags:
        print("Running smoke setup")

    if "regression" in scenario.tags:
        print("Running regression setup")
```

---

## Real Use Cases

- Browser setup and teardown
- Logging
- Screenshot on failure
- Environment switching
- Data setup

---

## Best Practices

- Keep hooks lightweight
- Avoid business logic in hooks
- Use hooks for setup/teardown only

---

## Common Mistakes

- Heavy logic inside hooks
- Not closing browser
- Overusing hooks

---

## Interview Answer

Hooks are lifecycle methods in BDD that execute setup and teardown logic before or after features, scenarios, or steps, enabling reusable and centralized test configuration.

---

## Generated On
2026-04-02 15:38:04.603525