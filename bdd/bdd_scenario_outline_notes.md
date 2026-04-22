# BDD Scenario Outline (Parameterized Testing Notes)

## Overview
Scenario Outline in Behave is used for data-driven testing.

It allows the same scenario to run multiple times with different input values.

---

## 1. What is Scenario Outline?

A Scenario Outline is a template scenario that uses placeholders for data.

The actual data is provided using the Examples table.

---

## 2. Basic Syntax

```
Scenario Outline: Login with multiple users
  When user enters username "<username>" and password "<password>"

Examples:
  | username | password |
  | user1    | pass1    |
  | user2    | pass2    |
```

---

## 3. Key Concepts

- Placeholders are written inside <> (angle brackets)
- Examples table provides test data
- Each row in Examples = 1 test execution

---

## 4. Example (Login)

```
Scenario Outline: Login with multiple credentials
  Given user is on login page
  When user enters username "<username>" and password "<password>"
  And clicks login button
  Then user should see "<result>"

Examples:
  | username     | password    | result     |
  | valid_user   | valid_pass  | dashboard  |
  | invalid_user | wrong_pass  | error      |
```

---

## 5. Step Definitions

```
@when('user enters username "{username}" and password "{password}"')
def step_enter_credentials(context, username, password):
    context.login_page.login(username, password)
```

```
@then('user should see "{result}"')
def step_validate(context, result):
    if result == "dashboard":
        assert "dashboard" in context.page.url
    elif result == "error":
        assert "error" in context.page.content()
```

---

## 6. Execution Flow

- Behave reads Scenario Outline
- Iterates through Examples rows
- Replaces placeholders with actual values
- Executes scenario multiple times

---

## 7. Advantages

- Reduces duplicate test cases
- Supports data-driven testing
- Improves readability
- Easy to scale

---

## 8. Best Practices

- Keep scenarios simple and readable
- Use meaningful column names
- Avoid too many columns
- Handle validation properly in step definitions

---

## 9. Common Mistakes

- Missing quotes around placeholders
- Mismatch between placeholder names and step definition parameters
- Writing logic in feature file
- Not handling multiple outcomes

---

## 10. Interview Answer

Scenario Outline is used for parameterized testing in BDD, where a single scenario is executed multiple times using different data sets defined in the Examples table.

---

## Generated On
2026-04-02 13:01:56.758841