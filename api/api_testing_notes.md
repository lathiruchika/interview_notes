# API Testing - Interview Notes

## 1. What is API Testing?

API Testing is the process of validating backend services by sending HTTP requests (GET, POST, PUT, DELETE) and verifying responses such as status code, response body, and headers without involving the UI.

---

## 2. Importance of API Testing

- Validates core backend business logic
- Detects defects early in development
- Ensures system reliability
- Independent of UI
- Faster and more stable than UI testing

---

## 3. Difference Between API Testing and UI Testing

| Aspect        | API Testing                         | UI Testing                        |
|--------------|-----------------------------------|----------------------------------|
| Layer        | Backend                           | Frontend                         |
| Speed        | Fast                              | Slow                             |
| Stability    | Stable                            | Flaky (wait/locator issues)      |
| Dependency   | No UI required                    | Depends on UI                    |
| Focus        | Data & business logic             | User experience & flow           |

---

## 4. Benefits of API Testing

- Faster execution (no browser)
- Early defect detection
- More stable (less flaky)
- Better test coverage (edge cases, negative scenarios)
- Validates business logic directly
- Easy to automate (Pytest, Requests, Postman)
- Can run even if UI is not ready

---

## 5. Quick Interview Summary

API Testing focuses on validating backend services by sending requests and verifying responses without UI. It is important because it ensures core functionality, detects defects early, and is faster and more reliable than UI testing. Compared to UI testing, API testing is more stable, faster, and independent of UI, making it ideal for CI/CD pipelines.
