# 🧭 Gherkin Language – Complete Notes

## ✅ 1. What is Gherkin?

**Definition:**  
Gherkin is a Domain-Specific Language (DSL) used in BDD (Behavior Driven Development) to write test cases in plain English.

**Purpose:**
- Bridge gap between Business, QA, and Developers
- Make test cases readable
- Convert requirements into executable tests

---

## ✅ 2. Gherkin Syntax Overview

### 🔑 Core Keywords

### 1️⃣ Feature
Describes high-level functionality

```gherkin
Feature: Login functionality
```

---

### 2️⃣ Scenario
Represents a single test case

```gherkin
Scenario: Successful login
```

---

### 3️⃣ Given / When / Then

```gherkin
Given user is on login page
When user enters valid credentials
Then user should be logged in
```

- Given → Precondition  
- When → Action  
- Then → Expected Result  

---

### 4️⃣ And / But

```gherkin
Given user is on login page
And user has valid account
When user enters username
And user enters password
Then user should see dashboard
```

---

## ✅ 3. Writing Feature Files

```gherkin
Feature: Login Feature

  Scenario: Successful login
    Given user is on login page
    When user enters valid username and password
    Then user should be redirected to dashboard
```

---

## 💡 Best Practices

- Use business language
- Keep scenarios short and clear
- One scenario = one behavior
- Avoid technical implementation details

---

## ✅ 4. Advanced Keywords

### Background

```gherkin
Background:
  Given user is on login page
```

---

### Scenario Outline

```gherkin
Scenario Outline: Login with multiple users
  Given user is on login page
  When user enters "<username>" and "<password>"
  Then user should see "<result>"

Examples:
  | username | password | result  |
  | user1    | pass1    | success |
  | user2    | wrong    | failure |
```

---

### Tags

```gherkin
@smoke
Scenario: Login test
```

Run with:
```
pytest -m smoke
```

---

## ✅ 5. Mapping to Automation

Flow:

Feature File → Step Definitions → Page Object Model → Assertions

---

### Example

#### Feature File
```gherkin
Scenario: Login
  Given user is on login page
  When user enters username and password
  Then user should see dashboard
```

---

#### Step Definition (pytest-bdd)

```python
@given("user is on login page")
def open_login_page(page):
    page.goto("login_url")

@when("user enters username and password")
def login(page):
    page.fill("#username", "test")
    page.fill("#password", "123")

@then("user should see dashboard")
def verify_dashboard(page):
    assert page.url == "dashboard_url"
```

---

## ✅ 6. Clean Scenario Writing

### ❌ Bad
```gherkin
Given user clicks login button using xpath
```

### ✅ Good
```gherkin
Given user clicks login button
```

---

## ✅ 7. Interview Summary

Gherkin is a DSL used in BDD to write test scenarios in a human-readable format using keywords like Feature, Scenario, Given, When, and Then. It helps bridge communication between business and technical teams and maps directly to automated tests.
