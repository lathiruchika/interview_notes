# 🚀 Python Generators – Complete Interview Notes

## 🧠 What is a Generator?
A generator is a function that:
- uses `yield`
- returns values one by one
- pauses and resumes execution

## 🎯 Key Properties
- Lazy (memory efficient)
- Maintains state
- Uses `yield`
- Single-use iterator
- `for` loop internally uses `next()`

## 🔥 Basic Example
def gen():
    print("start")
    yield 1
    print("middle")
    yield 2
    print("end")
    yield 3

## 🔁 Generator with Loop
def gen(n):
    for i in range(n):
        yield i

## 📦 Generator Expression
g = (x*x for x in range(5))

## 🔢 Square Generator
def square_gen(n):
    for i in range(1, n+1):
        yield i*i

## 🔍 Prime Generator
def gen_prime(n):
    for num in range(2, n+1):
        is_prime = True
        for i in range(2, int(num**0.5) + 1):
            if num % i == 0:
                is_prime = False
                break
        if is_prime:
            yield num

## ➕ Running Sum
def gen(lst):
    total = 0
    for num in lst:
        total += num
        yield total

## 🔁 Running Sum Reset
def gen(lst):
    total = 0
    for num in lst:
        if num < 0:
            total = 0
            yield total
        else:
            total += num
            yield total

## 📄 Word Generator
def word_gen(s):
    word = ""
    for ch in s:
        if ch != " ":
            word += ch
        else:
            if word:
                yield word
                word = ""
    if word:
        yield word

## 🧾 Log Filter
def error_logs(logs):
    for line in logs:
        if "error" in line.lower():
            yield line

## 📁 File Reader
def read_file(file_path):
    with open(file_path, "r") as file:
        for line in file:
            yield line

## 🎯 Interview Summary
- Lazy & memory efficient
- Uses yield
- Maintains state
- Single use
