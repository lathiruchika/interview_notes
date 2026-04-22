# 🔁 Python Generators with Loops — Interview Notes

---

## 🔹 1. Generator with Loop

```python
def gen(n):
    for i in range(n):
        yield i
```

---

## 🔹 2. How It Works

Example:

```python
g = gen(3)
```

👉 `range(3)` → 0, 1, 2

---

### Execution Flow

1. `g = gen(3)`
   → generator object created (no execution)

2. `next(g)`
   → yield 0

3. `next(g)`
   → yield 1

4. `next(g)`
   → yield 2

5. `next(g)`
   → StopIteration

---

## 🔹 3. Using list()

```python
g = gen(3)
print(list(g))
```

👉 Output:

```
[0, 1, 2]
```

---

## 🔹 4. Internal Working of list()

```python
result = []
while True:
    try:
        value = next(g)
        result.append(value)
    except StopIteration:
        break
```-------------------------------------------
or def gen(n):
    for i in range(n):
        yield i
        
g=gen(6)
result=[]
flag=True
while flag:
    try:
        value=next(g)
        result.append(value)
    except StopIteration as e:
        print("generator exhausted")
        flag=False
print(result)
            
            ----------------------------------------------------

👉 list() consumes generator completely

---

## 🔹 5. Important Concept (VERY IMPORTANT)

```python
g = gen(3)
print(list(g))   # [0, 1, 2]
print(list(g))   # []
```

👉 Generator is **exhausted after one use**

---

## 🔹 6. Key Interview Points

- Generators can be iterated only once
- After exhaustion → returns empty
- Uses lazy evaluation
- Works well for large datasets

---

## 🔹 7. Mental Model

```
Generator = Stream of data

Once consumed → gone
```

---

## 🚀 Summary

- Loop + yield → powerful lazy iteration
- list() → fully consumes generator
- Generator cannot be reused after exhaustion
--------------------------------------------------------------------------------------------------
