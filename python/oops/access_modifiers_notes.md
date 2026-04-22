# Python Access Modifiers & Encapsulation Notes (QA Automation)

## 1. Access Modifiers Overview

| Modifier | Syntax | Access | Use Case |
|----------|--------|--------|----------|
| Public | var | Everywhere | Actions, safe data |
| Protected | _var | Class + Child | Extensible behavior |
| Private | __var | Class only | Sensitive/internal data |

---

## 2. Public

- Accessible everywhere
- No restriction

Example:
```python
self.token = "123"
```

Use when:
- Safe to expose
- No risk in modification

---

## 3. Protected (_)

- Convention-based restriction
- Accessible in child classes
- Supports overriding

Example:
```python
self._token = "123"
```

Rules:
- Accessible in child
- Accessible outside (not recommended)

Use when:
- Method/variable needs extension

---

## 4. Private (__)

- Uses name mangling
- __var → _ClassName__var

Example:
```python
self.__token = "123"
```

Rules:
- Only accessible inside class
- Not directly accessible in child
- Can be accessed via _ClassName__var (not recommended)

Use when:
- Sensitive data
- Internal logic

---

## 5. Private Method Behavior

- Cannot be overridden
- Creates separate method in child

Example:
```python
def __log(self):
```

---

## 6. Protected Method Behavior

- Can be overridden
- Supports polymorphism

Example:
```python
def _log(self):
```

---

## 7. @property Decorator

Used for controlled access

Example:
```python
@property
def token(self):
    return self.__token
```

Behavior:
- Access like variable
- Internally calls method

---

## 8. @property.setter

Used to control modification

Example:
```python
@token.setter
def token(self, value):
    if value > 0:
        self.__token = value
```

---

## 9. Getter vs Setter

| Operation | Internal Call |
|----------|--------------|
| obj.token | getter |
| obj.token = value | setter |

---

## 10. Read-Only Property

If setter not defined:
- Attribute becomes read-only

---

## 11. Encapsulation Rules

- Hide data using private (__)
- Provide access via methods/property
- Avoid direct modification

---

## 12. Best Practices (Framework)

| Element | Modifier |
|--------|---------|
| click() | public |
| _wait() | protected |
| __generate_token() | private |
| token (read) | @property |

---

## 13. Interview Summary

- Private → avoid accidental access
- Protected → allow extension
- Public → open access
- @property → clean + controlled access
- setter → controlled modification

---

## 14. Key Takeaway

Public = Open  
Protected = Extendable  
Private = Hidden  
