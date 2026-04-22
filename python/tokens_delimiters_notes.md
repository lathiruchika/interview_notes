# 🧾 Tokens & Delimiters in Windows Batch (Jenkins Use Case)

## 🎯 Purpose
Used in batch scripts to **read and split text** (like `.env` files) into variables.

---

# 🔧 Basic Syntax

```bat
for /f "tokens=1,2 delims==" %%A in (file) do command
```

---

# 🔍 What is a Delimiter (`delims`)?

👉 A delimiter is a **character used to split a line**

### Example:
```env
BASE_URL=https://qa.example.com
```

Using:
```bat
delims==
```

Splits into:
- `BASE_URL`
- `https://qa.example.com`

---

# 🔍 What are Tokens?

👉 Tokens are the **parts after splitting**

```bat
tokens=1,2
```

Means:
- Token 1 → first part
- Token 2 → second part

---

# 🧩 Mapping

| Token | Variable | Value |
|------|--------|------|
| 1 | %%A | BASE_URL |
| 2 | %%B | https://qa.example.com |

---

# 🔁 Final Execution

```bat
set %%A=%%B
```

Becomes:
```bat
set BASE_URL=https://qa.example.com
```

✔ Now it's an environment variable

---

# 🚀 Full Jenkins Usage Example

```groovy
withCredentials([file(credentialsId: 'env-file', variable: 'ENV_FILE')]) {
    bat '''
    for /f "tokens=1,2 delims==" %%A in (%ENV_FILE%) do set %%A=%%B
    pytest
    '''
}
```

---

# ⚠️ Important Rules

## ✅ Correct Format
```env
KEY=value
```

## ❌ Wrong Format
```env
KEY = value   (spaces break parsing)
```

---

# ❌ Limitations

- Does NOT support:
  - Spaces around `=`
  - Multiline values
  - JSON format

---

# 🧠 Simple Understanding

- `delims` = how to split  
- `tokens` = which parts to take  

---

# 🧠 Interview Answer

In batch scripting, a delimiter defines how a string is split into parts, and tokens represent the extracted segments. For example, using `delims==` splits a `KEY=VALUE` pair into two tokens, which can then be assigned as environment variables.

---

# 🏁 Summary

| Term | Meaning |
|------|--------|
| Delimiter | Character used to split text |
| Tokens | Parts after splitting |
| %%A, %%B | Variables holding tokens |
| set %%A=%%B | Converts to env variable |
