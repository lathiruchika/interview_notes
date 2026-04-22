# 🚀 Pytest Framework Design Notes (Yield vs Finalizer vs Hooks + Roadmap)

---

# 🎯 Core Understanding

## Three Key Mechanisms in Pytest

| Tool | Scope | Purpose |
|------|------|--------|
| yield | Fixture | Simple setup & teardown |
| finalizer | Fixture | Flexible / multiple cleanup |
| hooks | Global | Test lifecycle control |

---

# 🥇 1. Yield (Simple Teardown)

### Use Case:
- Basic resource handling
- One setup → one teardown

```python
@pytest.fixture
def resource():
    setup()
    yield
    teardown()
```

### ✔ Pros:
- Clean
- Readable
- Default choice

---

# 🥈 2. Finalizer (Advanced Cleanup)

### Use Case:
- Multiple cleanup steps
- Conditional teardown
- Modular cleanup logic

```python
def cleanup_logs():
    print("Logs cleared")

def cleanup_screenshot():
    print("Screenshot taken")

request.addfinalizer(cleanup_logs)
request.addfinalizer(cleanup_screenshot)
```

### ✔ Pros:
- Multiple teardown functions
- Dynamic registration
- Execution order control (LIFO)

---

# 🥉 3. Hooks (Global Control)

### Example:

```python
def pytest_runtest_makereport(item, call):
```

### Use Case:
- Detect test pass/fail
- Reporting
- Framework-level behavior

---

# ⚔️ Comparison

| Feature | yield | finalizer | hooks |
|--------|------|----------|------|
| Simplicity | ⭐⭐⭐⭐ | ⭐⭐ | ⭐ |
| Flexibility | ⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐ |
| Multiple cleanup | ❌ | ✅ | ❌ |
| Conditional logic | ⚠️ | ✅ | ✅ |
| Access test result | ❌ | ⚠️ (via hook) | ✅ |

---

# 🧠 Golden Rule

```
yield → lifecycle
finalizer → modular cleanup
hooks → global awareness
```

---

# 🧱 Recommended Framework Pattern

## ✔ Use yield for:
- Browser
- Context
- Page

## ✔ Use finalizer for:
- Screenshot on failure
- Log cleanup
- Optional teardown logic

## ✔ Use hooks for:
- Test result detection
- Reporting integration

---

# 🔥 Combined Example

```python
@pytest.fixture
def page(context, request):
    page = context.new_page()

    def cleanup():
        if request.node.rep_call.failed:
            page.screenshot(path="fail.png")

    request.addfinalizer(cleanup)

    yield page

    page.close()
```

### Hook:

```python
@pytest.hookimpl(hookwrapper=True)
def pytest_runtest_makereport(item, call):
    outcome = yield
    rep = outcome.get_result()
    setattr(item, "rep_" + rep.when, rep)
```

---

# 🚀 Full Framework Roadmap

## Phase 1 — Logging
- Configure logging module
- File + console logs

## Phase 2 — Screenshot Hook
- Capture screenshot on failure

## Phase 3 — Config Management
- config.json
- Environment-based setup

## Phase 4 — Test Data
- JSON-based test data
- Parameterized tests

## Phase 5 — Page Expansion
- LoginPage
- HomePage

## Phase 6 — Utilities Layer
- logger.py
- config_reader.py
- data_reader.py

## Phase 7 — Parallel Execution
- pytest-xdist

## Phase 8 — Reporting
- Allure integration

---

# 📁 Final Structure

project/
├── pages/
├── tests/
├── config/
├── utils/
├── logs/
├── screenshots/
├── conftest.py
├── pytest.ini

---

# 🎯 Key Takeaway

- Do NOT choose one (yield vs finalizer vs hook)
- Use them together based on responsibility

---

# 🚀 Next Step

Implement Logging (Phase 1)
