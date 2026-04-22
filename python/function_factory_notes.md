# 🏭 Function Factory in Python

------------------------------------------------------------------------

## 🧠 Definition

A function factory is a function that returns another function, using
closures to retain data.

------------------------------------------------------------------------

## ✅ Basic Example

``` python
def multiplier(n):
    def inner(x):
        return x * n
    return inner
```

------------------------------------------------------------------------

## 🚀 Usage

``` python
double = multiplier(2)
triple = multiplier(3)

print(double(5))  # 10
print(triple(5))  # 15
```

------------------------------------------------------------------------

## 💡 Explanation

-   multiplier(2) creates a new function → double
-   double remembers n = 2
-   multiplier(3) creates another function → triple
-   Each function has its own stored value

------------------------------------------------------------------------

## 🔒 Closure Behind the Scenes

``` python
print(double.__closure__[0].cell_contents)  # 2
```

------------------------------------------------------------------------

## 🔑 Key Characteristics

-   Returns a function
-   Uses closure to store variables
-   Each returned function has independent state
-   Avoids global variables

------------------------------------------------------------------------

## 🎯 Real-World Example

``` python
def logger(prefix):
    def log(message):
        print(f"{prefix}: {message}")
    return log

info = logger("INFO")
error = logger("ERROR")

info("Test started")
error("Test failed")
```

------------------------------------------------------------------------

## ⚖️ Benefits

-   Reusability
-   Clean design
-   State retention

------------------------------------------------------------------------

## 🚀 Interview One-Liner

A function factory creates and returns another function, using closures
to retain and customize behavior.
