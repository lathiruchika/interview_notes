# 🧪 Pytest Notes (Quick + Deep Revision)

---

## 1. What is Pytest?
- Python testing framework
- Simple syntax (no class required)
- Auto test discovery
- Powerful features: fixtures, parametrization, hooks

### Why better than unittest?
| Feature | pytest | unittest |
|--------|--------|----------|
| Syntax | Simple (assert) | Verbose |
| Fixtures | Powerful | Limited |
| Parametrization | Built-in | Not native |
| Plugins | Huge ecosystem | Limited |

---

## 2. Basic Test Example
```python
def func(x):
    return x + 1

def test_sample():
    assert func(3) == 4
```

---

## 3. Assertions in Pytest
```python
assert a == b
assert x > 0
```

### Custom Message
```python
assert a == b, "Values are not equal"
```

### Hard vs Soft Assertion
- Pytest → only hard assertions by default
- Soft assertion → use plugins (pytest-check)

---

## 4. Fixtures
Reusable setup/teardown logic

```python
import pytest

@pytest.fixture
def setup():
    print("Setup")
    yield
    print("Teardown")
```

### Usage
```python
def test_example(setup):
    assert True
```

---

## 5. Fixture Scope
| Scope | Meaning |
|------|--------|
| function | Default, runs per test |
| class | Per class |
| module | Per file |
| session | Entire run |

```python
@pytest.fixture(scope="session")
def db():
    return "DB Connection"
```

---

## 6. Parametrization

```python
@pytest.mark.parametrize("a,b,result", [(1,2,3), (2,3,5)])
def test_add(a,b,result):
    assert a + b == result
```

### Using fixture params
```python
@pytest.fixture(params=["chrome", "firefox"])
def browser(request):
    return request.param
```

---

## 7. Markers

### Skip Test
```python
@pytest.mark.skip(reason="Not ready")
```

### Skip Dynamically
```python
import pytest

if condition:
    pytest.skip("Skipping test")
```

### Markers need registration (pytest.ini)
```ini
[pytest]
markers =
    smoke
    regression
```

---

## 8. Hooks vs Fixtures

### Fixtures
- Used for setup/teardown
- Injected into tests

### Hooks
- Modify pytest behavior
- Global control

Example:
```python
@pytest.hookimpl(hookwrapper=True)
def pytest_runtest_makereport(item, call):
    outcome = yield
    report = outcome.get_result()
```

---

## 9. Worker ID (Parallel Execution - xdist)

### Method 1: request object
```python
@pytest.fixture
def worker_id(request):
    if hasattr(request.config, "workerinput"):
        return request.config.workerinput["workerid"]
    return "gw0"
```

### Method 2: Environment variable
```python
import os

def get_worker_id():
    return os.getenv("PYTEST_XDIST_WORKER", "gw0")
```

---

## 10. request Object
- Built-in fixture
- Gives access to:
  - config
  - params
  - node info

Example:
```python
def test_example(request):
    print(request.node.name)
```

---

## 11. addoption (CLI Arguments)

```python
def pytest_addoption(parser):
    parser.addoption("--env", action="store", default="dev")
```

### Access value
```python
@pytest.fixture
def env(request):
    return request.config.getoption("--env")
```

---

## 12. Fixture Scope Conflict Issue
Problem:
- function fixture used inside session fixture

Error:
```
ScopeMismatch: You tried to access function scoped fixture
```

Solution:
- Make scopes same OR
- Reduce higher scope

---

## 13. Sharing Data Across Tests

### Using Fixtures
```python
@pytest.fixture(scope="session")
def shared_data():
    return {}
```

### Using Classes
```python
class Test:
    data = {}
```

---

## 14. Rerun Failed Tests

Plugin:
```
pip install pytest-rerunfailures
```

```bash
pytest --reruns 2
```

---

## 15. Exception Handling in Pytest

```python
import pytest

with pytest.raises(ValueError):
    int("abc")
```

---

## 16. Debugging Tips

- Use `-s` → print logs
- Use `--pdb` → debug on failure
- Use logging instead of print

```bash
pytest -s --pdb
```

---

## 17. Important Concepts Summary

### Must Know (Interview)
- Fixtures & scope
- Parametrization
- Hooks vs fixtures
- request object
- pytest_addoption
- Parallel execution (xdist)

### Framework Level Concepts
- Multi-user handling
- Environment-based config
- Logging + Allure integration

---

## 18. Your Framework Improvements (Today)

- users.json for multi-user handling
- config.ini for environments
- worker_id for parallel isolation
- CLI control for env/user
- Allure logging improvements

---

## 🚀 Final Tip
Focus on:
- Understanding flow (fixture → test → hook)
- Not just syntax
- Debugging ability

---

🔥 You covered a LOT today. Revise this once before interview.

