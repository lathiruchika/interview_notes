# 🚀 API Testing & HTTP Fundamentals (Interview Notes)

---

# 1. What is API?

API (Application Programming Interface) is a mechanism that allows two systems to communicate by sending requests and receiving responses.

---

# 2. What is API Testing?

API Testing is the process of validating backend services by sending HTTP requests and verifying responses without involving UI.

---

# 3. Importance of API Testing

- Validates core business logic
- Detects defects early
- Faster and more stable than UI testing
- Independent of UI
- Easy to automate

---

# 4. Client-Server Architecture

Client → sends request  
Server → processes request + sends response  

### 3-Tier Architecture
Client → Application Server (API) → Database

- Client: UI / Test Script
- API Layer: Business Logic
- Database: Data Storage

---

# 5. What is HTTP?

HTTP (HyperText Transfer Protocol) is used for communication between client and server.

---

# 6. HTTP Request

HTTP Request = Method + URL + Headers + Body

---

# 7. HTTP Response

HTTP Response = Status Code + Headers + Body

---

# 8. HTTP Methods

| Method | Purpose               |Body| Idempotent | Example |
|--------|-----------------------|----|------------|--------|
| GET    | Fetch data            | ❌ | ✔️        | GET /users |
| POST   | Create data           | ✔️ | ❌        | POST /users |
| PUT    | Update full data      | ✔️ | ✔️        | PUT /users/1 |
| DELETE | Delete data           | ❌ | ✔️        | DELETE /users/1 |
| PATCH  | Partial update        | ✔️ | ❌        | PATCH /users/1 |
| OPTIONS| Check allowed methods | ❌ | ✔️        | OPTIONS /users |

---

# 9. API Endpoints

Endpoint = API URL where request is sent

Example:
- /users → all users
- /users/1 → specific user

---

# 10. Headers

Headers are key-value pairs providing metadata.

Examples:
- Authorization
- Content-Type
- Accept

---

# 11. HTTP Status Codes

## 🔹 Categories

| Category | Meaning |
|----------|--------|
| 1xx | Informational |
| 2xx | Success |
| 3xx | Redirection |
| 4xx | Client Error |
| 5xx | Server Error |

---

# 12. Important Status Codes

| Code | Description | Method Example | Real-Life Analogy |
|------|------------|---------------|------------------|
| 100 | Continue | File upload | "Go ahead, continue" |
| 200 | OK | GET | Got your order |
| 201 | Created | POST | New dish prepared |
| 202 | Accepted | Async job | Will prepare later |
| 204 | No Content | DELETE | Nothing to return |
| 301 | Moved Permanently | URL change | Restaurant shifted |
| 302 | Temporary Redirect | Temporary routing | Go there for now |
| 304 | Not Modified | Caching | Same food, reuse |
| 400 | Bad Request | Invalid input | Wrong order |
| 401 | Unauthorized | No auth | Who are you? |
| 403 | Forbidden | No permission | Not allowed |
| 404 | Not Found | Wrong endpoint | Item not on menu |
| 405 | Method Not Allowed | Wrong method | Wrong way to order |
| 409 | Conflict | Duplicate data | Duplicate order |
| 422 | Validation error | Invalid data | Wrong format |
| 500 | Server Error | Server crash | Kitchen failure |
| 502 | Bad Gateway | Server chain error | Middleman failed |
| 503 | Service Unavailable | Server down | Restaurant closed |

---

# 🔁 Memory Tricks

- 2xx → Success
- 3xx → Redirect
- 4xx → Client mistake
- 5xx → Server mistake

---

# 🎯 Final Interview Summary

API testing validates backend services by sending HTTP requests and verifying responses. It is faster, more stable, and helps detect defects early. HTTP enables communication between client and server using methods like GET, POST, PUT, and DELETE. Status codes indicate the result of the request, categorized into success, redirection, client errors, and server errors.
