# Python zip() Notes

## Definition

zip() combines multiple iterables element-wise.

## Syntax

zip(iterable1, iterable2, ...)

## Example

names = \["Alice", "Bob"\] scores = \[85, 90\] print(list(zip(names,
scores))) \# \[('Alice', 85), ('Bob', 90)\]

## Key Points

-   Stops at shortest iterable
-   Returns iterator
-   Useful for pairing data

## Convert to dict

keys = \["id", "name"\] values = \[1, "Test"\] print(dict(zip(keys,
values)))

## Trick

z = zip(\[1,2\], \[3,4\]) print(list(z)) print(list(z)) \# empty
