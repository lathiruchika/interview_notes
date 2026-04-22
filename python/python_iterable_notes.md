# Python Iterable --- Clean Notes

------------------------------------------------------------------------

## 🔹 1. What is Iterable?

An **iterable** is an object that can be looped over (traversed) and can
return an iterator using `iter()`.

------------------------------------------------------------------------

## 🔹 2. Key Characteristics

-   Has `__iter__()` method
-   Can be used in `for` loop
-   Cannot use `next()` directly
-   Returns an iterator

------------------------------------------------------------------------

## 🔹 3. Examples of Iterable

``` python
lst = [1,2,3]        # list
tup = (1,2,3)        # tuple
s = "hello"          # string
st = {1,2,3}         # set
d = {"a":1, "b":2}   # dictionary
r = range(5)         # range
```

------------------------------------------------------------------------

## 🔹 4. Using iter()

``` python
lst = [1,2,3]
it = iter(lst)   # converts iterable → iterator
```

------------------------------------------------------------------------

## 🔹 5. Iterable vs Iterator

  Feature   Iterable     Iterator
  --------- ------------ ------------------------
  Method    **iter**()   **iter**(), **next**()
  next()    ❌ No        ✅ Yes
  Purpose   Collection   Value generator

------------------------------------------------------------------------

## 🔹 6. Why next() fails on iterable

``` python
lst = [1,2,3]
next(lst)   # ❌ TypeError
```

👉 Because iterable does not have `__next__()`

------------------------------------------------------------------------

## 🔹 7. for loop behavior

``` python
for i in lst:
    print(i)
```

Internally:

``` python
it = iter(lst)
next(it)
```

------------------------------------------------------------------------

## 🔹 8. Important Concepts

-   Iterable can create multiple iterators
-   Iterable does not store iteration state
-   Iterator handles the state

------------------------------------------------------------------------

## 🔹 9. Example to Understand

``` python
lst = [10,20,30]

it1 = iter(lst)
it2 = iter(lst)

print(next(it1))  # 10
print(next(it2))  # 10 (independent iterator)
```

------------------------------------------------------------------------

## 🔹 10. Interview Points

-   Iterable = object that can be iterated
-   Must implement `__iter__()`
-   Used in loops
-   Cannot use `next()` directly

------------------------------------------------------------------------

## 🔹 Final Summary

-   Iterable = container (list, tuple, string)
-   Iterator = object that gives next values
-   `iter()` converts iterable → iterator

------------------------------------------------------------------------

🚀 You are interview ready!
