# 📊 Pandas Complete Interview Notes (Detailed)

------------------------------------------------------------------------

# 1. SERIES

## Concept (Layman)

A Series is like a single column in Excel.

## Example

``` python
import pandas as pd
s = pd.Series([10,20,30])
```

## Diagram

Index → 0 1 2\
Values →10 20 30

## Key Points

-   1D structure
-   has index + values
-   supports multiple data types

## Interview Answer

A Series is a one-dimensional labeled array capable of holding various
data types.

------------------------------------------------------------------------

# 2. DATAFRAME

## Concept

Table with rows and columns.

## Example

``` python
df = pd.DataFrame({
    "name":["A","B"],
    "age":[25,30]
})
```

## Diagram

  index   name   age
  ------- ------ -----
  0       A      25
  1       B      30

## Key Points

-   2D structure
-   collection of Series

## Interview Answer

A DataFrame is a two-dimensional labeled data structure.

------------------------------------------------------------------------

# 3. INDEXING (loc vs iloc)

## loc (label based)

``` python
df.loc[0]
```

## iloc (position based)

``` python
df.iloc[0]
```

## Difference

-   loc → inclusive
-   iloc → exclusive

------------------------------------------------------------------------

# 4. FILTERING

## Example

``` python
df[df["age"]>25]
```

## Multiple Conditions

``` python
df[(df["age"]>25) & (df["salary"]>50000)]
```

## Diagram

Condition → True/False → Filter rows

## Interview Answer

Boolean indexing is used to filter rows based on conditions.

------------------------------------------------------------------------

# 5. SLICING

## Example

``` python
df.iloc[0:2]
```

## Rule

-   start included
-   end excluded

------------------------------------------------------------------------

# 6. GROUPBY

## Concept

Split → Apply → Combine

## Example

``` python
df.groupby("dept")["salary"].mean()
```

## Diagram

IT → \[50000,70000\] → avg\
HR → \[40000,45000\] → avg

## Interview Answer

GroupBy splits data into groups and applies aggregation functions.

------------------------------------------------------------------------

# 7. MULTIPLE AGGREGATION

``` python
df.groupby("dept")["salary"].agg(["sum","mean","count"])
```

------------------------------------------------------------------------

# 8. MERGE (JOIN)

## Types

-   inner → common
-   left → all left
-   right → all right
-   outer → all

## Example

``` python
pd.merge(df1, df2, on="id", how="left")
```

## Diagram

df1 → 1,2,3\
df2 → 1,2,4

LEFT → 1,2,3

## Interview Answer

Merge combines DataFrames similar to SQL joins.

------------------------------------------------------------------------

# 9. MISSING VALUES

## Example

``` python
df.isnull()
df.fillna(0)
```

## Concept

NaN → missing data

------------------------------------------------------------------------

# 10. IMPORTANT INTERVIEW POINTS

-   loc vs iloc
-   filtering syntax
-   groupby + agg
-   joins
-   NaN handling

------------------------------------------------------------------------

# 🚀 FINAL TIP

Focus on: - filtering - groupby - merge

These are most asked in interviews.
