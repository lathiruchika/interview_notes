# Pandas Interview Notes (Quick Revision)

## 1. Series

### Concept

1D labeled array.

### Example

``` python
s = pd.Series([10,20,30])
```

### Interview Answer

Series is a one-dimensional labeled data structure in Pandas.

------------------------------------------------------------------------

## 2. DataFrame

### Concept

2D table (rows + columns)

### Example

``` python
df = pd.DataFrame({"name":["A","B"],"age":[25,30]})
```

### Interview Answer

A DataFrame is a two-dimensional labeled data structure similar to a
table.

------------------------------------------------------------------------

## 3. Filtering

### Example

``` python
df[df["age"]>25]
```

### Interview Answer

Boolean indexing is used to filter rows based on conditions.

------------------------------------------------------------------------

## 4. GroupBy

### Concept

Split → Apply → Combine

### Example

``` python
df.groupby("dept")["salary"].mean()
```

### Interview Answer

GroupBy groups data and applies aggregation functions.

------------------------------------------------------------------------

## 5. Merge

### Types

-   inner
-   left
-   right
-   outer

### Example

``` python
pd.merge(df1, df2, on="id", how="left")
```

### Interview Answer

Merge combines DataFrames based on a common column similar to SQL joins.

------------------------------------------------------------------------

## 6. Key Interview Points

-   loc vs iloc
-   boolean indexing
-   groupby aggregations
-   joins
-   NaN handling
