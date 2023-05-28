[toc]

# Statistics and Delete
Statistics
```python3
df.isna()
df.isna.mean()
```
Delete
```python3
df.dropna(axis, how, subset)
df.dropna(axis, thresh)
```

**Usage 1**
`subset` is a list of indexes(or columns). \
`how` is a str in ['any', 'all'],
it indicates 
when any or all indexes(or columns) in `subset`,
delete this column(or row).

**Usage 2**
`thresh` is a threshold value, 
when the num of not nan is lower than `thresh`,
delete this row(or column).

# Fill and Interpolate
Fill
```python3
s.fillna(method, limit)
s.fillna(value)
s.fillna(dict[index:value])
```
`method` is a str in ['ffill', 'bfill'], 
filling back with previous values or filling forward with following values.\
`limit` is the max of consecutively filling, default no limit.

Interpolate

```python3
s.interpolate(method, limit_direction, limit)
```
`method` : str in ['linear', 'index', 'nearest'], default 'linear'. Interpolation technique to use.\
`limit` : int, optional. Maximum number of consecutive NaNs to fill.\
`limit_direction` : {{'forward', 'backward', 'both'}}, Optional. Consecutive NaNs will be filled in this direction.


# Nullable

## Normal Missing
In normal series, `np.nan` is `NaN`, a float type. 
In time series, `np.nan` is converted to `NaT`, a datatime type.
```python3
np.nan == np.nan  # False
np.nan is None  # False
np.nan is False  # False

pd.Series([np.nan]).equals(pd.Series([np.nan])) # True
```
For `equals` method, `np.nan` is equivalent to another `np.nan`.

## Nullable Series
A new nan class `pd.NA`, which has not a fixed type. \
The bool calculations of `pd.NA` are more logical.
```python3
pd.NA | True # True
pd.NA & False # False
~pd.NA # pd.NA, if result is uncertain
```
The arithmetic operation of `pd.NA`
```python3
pd.NA ** 0 # 1
1 ** pd.NA # 1
```

Three nullable types of series, `Int64`, `boolean`, `string`.
```python3
pd.Series([np.nan, 1], dtype='Int64')
pd.Series([np.nan, True], dtype = 'boolean')
pd.Series([np.nan, 'my_str'], dtype = 'string')
```
A calculation of nullable series returns a nullable series as much as possible.

When reading files, we could use
```python3
df = pd.read_csv(file_name)
df = df.convert_dtypes()
```
to make it nullable.

