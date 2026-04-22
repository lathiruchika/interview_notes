# Python filter() Notes

## Definition

filter() selects elements based on condition.

## Syntax

filter(function, iterable)

## Example

nums = \[1,2,3,4,5\] print(list(filter(lambda x: x%2==0, nums))) \#
\[2,4\]

## Key Points

-   Returns iterator
-   Needs list() to view
-   Used for filtering

## Trick

nums = \[0,1,2,"",None,3\] print(list(filter(None, nums))) \# \[1,2,3\]
