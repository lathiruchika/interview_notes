# BDD Framework Implementation (Behave + Playwright + Logger)

## Overview
This document captures the complete implementation of a BDD framework using:
- Behave (BDD)
- Playwright (UI automation)
- Page Object Model (POM)
- Custom Logger (LoggerFactory)

---

## Project Structure

```
your_project/
│
├── features/
│   ├── login.feature
│   ├── environment.py
│   └── steps/
│       └── login_steps.py
│
├── pages/
│   └── login_page.py
│
├── utils/
│   └── logger.py
```

---

## 1. Feature File (Gherkin)

`features/login.feature`

```
Feature: Login functionality

  Scenario: Successful login
    Given user is on login page
    When user enters valid username and password
    And clicks login button
    Then user should be redirected to dashboard
```

---

## 2. Logger Implementation

`utils/logger.py`

```python
import logging

class LoggerFactory:
    _loggers = {}

    @staticmethod
    def get_logger(name):
        if name not in LoggerFactory._loggers:
            logger = logging.getLogger(name)
            logger.setLevel(logging.INFO)

            ch = logging.StreamHandler()
            formatter = logging.Formatter(
                "%(asctime)s - %(name)s - %(levelname)s - %(message)s"
            )
            ch.setFormatter(formatter)

            logger.addHandler(ch)

            LoggerFactory._loggers[name] = logger

        return LoggerFactory._loggers[name]
```

---

## 3. Environment Setup (Hooks)

`features/environment.py`

```python
from playwright.sync_api import sync_playwright
from utils.logger import LoggerFactory

def before_all(context):
    context.logger = LoggerFactory.get_logger("GLOBAL")
    context.logger.info("Starting Test Execution")

    context.playwright = sync_playwright().start()

def before_scenario(context, scenario):
    context.logger = LoggerFactory.get_logger(scenario.name)
    context.logger.info(f"Starting Scenario: {scenario.name}")

    context.browser = context.playwright.chromium.launch(headless=False)
    context.context = context.browser.new_context()
    context.page = context.context.new_page()

def after_scenario(context, scenario):
    context.logger.info(f"Finished Scenario: {scenario.name}")
    context.browser.close()

def after_all(context):
    context.logger.info("Test Execution Completed")
    context.playwright.stop()
```

---

## 4. Step Definitions

`features/steps/login_steps.py`

```python
from behave import given, when, then
from pages.login_page import LoginPage

@given("user is on login page")
def step_open_login(context):
    context.logger.info("Opening login page")
    context.login_page = LoginPage(context.page, context.logger)
    context.login_page.open()

@when("user enters valid username and password")
def step_enter_credentials(context):
    context.logger.info("Entering credentials")
    context.login_page.login("testuser", "password123")

@when("clicks login button")
def step_click_login(context):
    context.logger.info("Clicking login button")
    context.login_page.click_login()

@then("user should be redirected to dashboard")
def step_validate_dashboard(context):
    context.logger.info("Validating dashboard")
    assert "dashboard" in context.page.url
```

---

## 5. Page Object Model

`pages/login_page.py`

```python
class LoginPage:

    def __init__(self, page, logger):
        self.page = page
        self.logger = logger

        self.username = "#username"
        self.password = "#password"
        self.login_btn = "#login"

    def open(self):
        self.logger.info("Navigating to login page")
        self.page.goto("https://example.com/login")

    def login(self, user, pwd):
        self.logger.info(f"Entering username: {user}")
        self.page.fill(self.username, user)
        self.page.fill(self.password, pwd)

    def click_login(self):
        self.logger.info("Clicking login button")
        self.page.click(self.login_btn)
```

---

## 6. Execution Command

```
behave
```

---

## 7. Key Concepts

- `context` is used to share objects across steps
- Logger is injected via `context.logger`
- Page Objects handle UI logic
- Step Definitions map Gherkin to Python
- Hooks manage setup/teardown

---

## 8. Best Practices

- Do not import logger in step files
- Use `context` for shared objects
- Keep step definitions clean
- Keep logic in page objects
- Use scenario-based logging

---

## Generated On
2026-04-02 10:54:24.307474