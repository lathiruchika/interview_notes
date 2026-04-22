# 🚀 Python Generators – Complete Rules & Notes

---

# 🔹 What is a Generator?

A **generator** is a function that:
- uses `yield`
- returns values **one at a time**
- remembers its state

---

# 🔑 Rule 1: Use `yield` (not `return`)
- `yield` → pauses function
- `return` → ends function

---

# 🔑 Rule 2: Execution pauses and resumes
- Generator pauses at `yield`
- Resumes from next line

---

# 🔑 Rule 3: Generator does NOT execute immediately
- Runs only when `next()` or loop is used

---

# 🔑 Rule 4: Use `next()` to get values
- Each `next()` runs until next `yield`

---

# 🔑 Rule 5: StopIteration (Base Condition)
- Raised when generator is exhausted

---

# 🔑 Rule 6: Memory Efficient
- Generates values one by one
- Does not store full data

---

# 🔑 Rule 7: Works with loops
- `for` loop automatically handles iteration

---

# 🔑 Rule 8: Generator is an Iterator
- Has __iter__() and __next__()

---

# 🔑 Rule 9: Multiple yield allowed

---

# 🔑 Rule 10: Can use conditions
- Useful for filtering (e.g., logs)

---

# 🔑 Rule 11: Generator Expression
- Syntax: (expression for item in iterable)

---

# 🔑 Rule 12: return in generator
- Stops execution
- Raises StopIteration

---

# 🧠 Mental Model

Generator = function + yield + state memory

next() → run till next yield  
yield → pause  
resume → continue  
end → StopIteration  

---

# 🔥 Interview One-Liner

A generator is an iterator that produces values lazily using `yield` and maintains its state.
