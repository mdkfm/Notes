[toc]
## Pandas Tools
1. xlrd 
2. openpyxl 
3. tabulate 
4. pandas_profiling

## File reading and writing functions
### Read function
`pandas` could read many kinds of file，such as `csv, excel, txt`.
```python3
import pandas as pd
df_csv = pd.read_csv('file.csv')
df_table = pd.read_table('file.txt') 
df_excel = pd.read_excel('file.xlsx')
```
#### Shared parameters
1. `header: str = "infer"` denotes that the first line is not col name.
2. `index_col` denotes that it makes some cols as index.
3. `usecols` is the set of cols which we will read.
4. `parse_dates` indicates that the cols would be read as time.
5. `nrows` is the num of rows read.

#### Private paramters
##### `pd.read_table()`
`sep` is the Separator with regular expression. \
We should use the parameter `engine='python'` at the same time.

### Writing function
```python3
df.to_csv('file.csv', sep='\t')
df.to_excel('file.xlsx')
df.to_markdown('file.md')
df.to_latex()
```
`index=False` removes indices. 
The function `df.to_csv()` have a `sep` parameter to select a separator. \
The functions `df.to_markdown()` and `df.to_latex()` need a pre-package `tabulate` 

## Series and Dataframe
### Series
`pd.Series` is a kind of data structure consisted of four parts
1. `data`, the values of series
2. `index`, the index (with a name or without) 
3. `dtype`, the date type
4. `name`, the name of series

### Dataframe
`Dataframe` is a table.
DataFrame has added column indexes on top of Series, i.e.`columns`.

### Normal Attributes
```python3
df.values # return all value
df.index # return all index
df.columns # return all column indexs
df.dtypes # return all dtypes corresponding 
df.shape # return the shape
df.T # return the transposition of df
```

### Normal function
```python3
df.set_index(cols)
```

## Aggregation function
Sampling
```python3
df.head(n) # take the previous n rows
df.tail(n) # take the last n rows
```
Global features
```python3
df.info() # information overview
df.describe() # main statistics
```
More, we need the package [pandas-profiling](https://pandas-profiling.github.io/pandas-profiling/docs/).

## Statistics function
1. `sum, mean`
2. `median, quantile`
3. `var, std`
4. `max, min, idxmax, idmin`
5. `count`

along parameter `axis`

## Unique function
```python3
df[cols].unique() # unique cols
df[cols].nunique() # num of unique cols
df[cols].value_counts()
df[cols].drop_duplicates(keep='first'|'last'|'false') # remove duplicates
df[cols].duplicated(keep='first'|'last'|'false') # bool sequence
```
`drop_duplicates` removes element according to `duplicated`.

## Replace function
```python3
s.replace(to_replace: list, value: list)
s.replace(d: dict[to_replace, value])

s.where(bs: bool series, value) # replace false
s.mask(bs: bool series, value) # replace true

s.round()
s.abs()
s.clip(inf: num, sup: num) # replace lower and higher with inf or sup
```

## Sort function
```python3
df.sort_index(indexs, ascending: bool series)
df.sort_values(level = cols, ascending: bool series = bs)
```

## `apply` function
```python3
df.apply(func)
df.apply(lambda)
```
input: every column one by one (pd.Series) 
output: a series as a column 

## Windows function
```python3
s.rolling(window: int = len) 
s.expanding()
s.ewm(alpha: num = coefficient)
```
