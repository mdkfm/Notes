[toc]

## GroupBy
```python3
df.groupby(cols, dropna)
df.groupby(condition)
```
`cols`, str or list.\
`condition`, series of group names, matching rows.\
`dropna` is a bool value,
indicating whether regard `NaN` as a group.\
Return a `DataFrameGroupBy` or `SeriesGroupBy`.

`GroupBy[cols]` return a `GroupBy`.

### attributes
`ngroups`, num of groups. \
`groups`, dict[group_name, index]. \

function:
`size`, size of groups. \
`get_group`, get group in origin data.

## Aggregate function
All return a new dataframe.

Normally:
1. `max`, `min`, `idxmax`, `idxmin`
2. `mean`,  `sum`, `prod`, `std`, `var`, `size`, `count`, `nunique`
3. `all`, `any` 
4. `median`, `quantile`
5. `sem`, standard error of the mean of groups.
6. `skew`, unbiased skew.

### `agg`
`gb.agg(list)`, `list`, a list of function name. \
`gb.agg(dict)`, `dict`, dict[col_name, List[func] | List[(name, func)]].

`agg` returns dataframe with origin col and `func.__name__`(name) as column.

Inner function input: column in group; \
output: a aggregate value

## Transform function
Transform the origin dataframe.

Normally, `cumcount`, `cumsum`, `cumprod`, `cummax`, `cummin`

### `transform`
`gb.transform(func)` \
`func`, input: a column in group; output: a column in group. \
The function puts inner output together as output. 

## Filter function
`gb.filter(func)` \
`func`, input: a column in group; output: a series of bool.\
The function filters data according the inner output.

## `apply`
`gb.apply(func)`\
`func`, input: a dataframe in group; output: scalar | Series | DataFrame.\
`apply` will automatically split joint the inner output.