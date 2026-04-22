# 🔍 Generalized Data Extraction from Unpredictable API Responses

## 🎯 Problem
API responses can be unpredictable and deeply nested:
- dict
- list
- nested combinations (dict inside list, list inside dict)
- primitive values (string, int, etc.)

We need a **generic way to extract a value (e.g., `id`) from anywhere in the response**.

---

## 🧠 Approach
Use **recursive traversal**:
- If dict → check keys, then traverse values
- If list → iterate items and traverse
- If primitive → ignore

---

## ✅ Generalized Function

```python
def find_key(data, target_key):
    """
    Recursively search for a key in nested JSON (dict/list).
    """

    if isinstance(data, dict):
        if target_key in data:
            return data[target_key]

        for value in data.values():
            result = find_key(value, target_key)
            if result is not None:
                return result

    elif isinstance(data, list):
        for item in data:
            result = find_key(item, target_key)
            if result is not None:
                return result

    return None
```

---

## 💻 Usage Example

```python
import requests

response = requests.get("https://jsonplaceholder.typicode.com/users")
data = response.json()

user_id = find_key(data, "id")

print(user_id)
```

---

## 🧠 What This Handles

✔ Nested dictionaries  
✔ Lists inside dictionaries  
✔ Dictionaries inside lists  
✔ Deeply nested structures  
✔ Safe (no crash if key not found)  

---

## 🔁 Memory Trick

👉 Dict → check + go deeper  
👉 List → loop + go deeper  
👉 Recursion = repeat same logic  

---

## 🎯 Interview Answer

To handle unpredictable API responses, we can use a recursive function that checks whether the data is a dictionary or list and traverses it to find the required key safely.
