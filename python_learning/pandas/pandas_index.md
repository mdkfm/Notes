[toc]

## Index
`pd.Index`, `pd.MultiIndex`\
`df.index`, `df.column`

Note: we could assign after more than one layer indexer

### Set index
`df.set_index()`

### `loc` element indexer

`df.loc[*]` is `df.loc[row]`. \
`df.loc[*, *]` is `df.loc[row, col]`.\
`*` is 
1. only one element
2. list of elements
3. element slice
4. list of bool value
5. function (or lamda): input:df; output: belong above

### `iloc` position indexer
`df.iloc[*]` is `df.iloc[row]`. \
`df.iloc[*, *]` is `df.iloc[row, col]`.\
`*` is
1. only one int
2. list of ints
3. int slice
4. list of bool value
5. function (or lamda): input:df; output: belong above

### `query` function
Similar to `eval` function. \
`df.query(*)`, `*` is a legal query expression.\
Legal expressions or registered variates:
1. all column names
2. '\`column name\` == [1, 2, 3]' ('==' is equivalent to 'in')
3. '@variate' (variate defined outer query)

### Random sample
```python3
df.sample(size, replace, weights)
```
`size`, a int.\
`replace`, a bool.\
`weights`, a list of weight.\
`replace` indicates whether put element back.\
`weights` is relative probability.

### `get_indexer`
Search indexes in `df.index`.
```python3
df.index.get_indexer(target, method)
```
`target`, a `pd.Index` or a value as target.\
`method`, ['pad', 'backfill', 'nearest'], search method, default `None`.


## `MultiIndex`
A value of a `MultiIndex` is a tuple.

We could not change the values of index directly. \
```python3
pd.get_level_values(n)
```
It gets values of nth layer. 

### `loc` and `iloc` indexer
Before we used indexer, we should sort the indexes.
```python3
df.sort_index(axis=0) # sort index
df.sort_index(axis=1) # sort column
```

Particularly, `*` cloud be:
1. `(list_level_0, list_level_1, ...)`, Cartesian product of lists.
2. `[index_tuple_1, index_tuple_2, ...]`, list of `MultiIndex`. 
3. `IndexSlice`

#### `IndexSlice`
```python3
idx = pd.IndexSlice
```
Use `idx` to call the `pd.IndexSlice` function. \
`idx[*, *, ...]`, `*` corresponds to one layer `MultiIndex`. \
The content of `*` is determined by outer indexer.

### Construct method
```python3
pd.MultiIndex.from_tuples(tuples, names)
pd.MultiIndex.from_arrays(arrays, names)
pd.MultiIndex.from_product(lists, names)
```
`from_tuples` from a tuple list, a tuple is a `MultiIndex`. \
`from_arrays` from a list of lists, a list is a layer index. \
`from_product` uses Cartesian product of lists.

### Change
`axis` is `1` or `0`. `0` is row, `1` is column.

#### `map`
`df.index.map(function)`

#### Swap
`df.swaplevel(level_1, level_2, axis)`.\
`df.reorder_levels(level_list, axis)`, reorders all levels according to `level_list`.

#### Drop
`df.droplevel(droped, axis)`, `droped` could be a int or list of ints.

#### Change attributes

##### change name
`df.rename_axis(index=change_index, column=change_column)`,
`change_index` and `change_column` could be a `dict[to_replace: value]`, or a function.

##### change value
`df.rename(index=change_index, level=change_level)`,
`df.rename(column=change_column, level=change_level)` \
`change_index` and `change_column` could be a `dict[to_replace: value]`, or a function.\
`change_level` is the order num of changed layer.

#### set and reset
`df.set_index(indexes, append)` \
`indexes` is only a column name or list. \
`append` indicates whether keep origin indexes as inner.

`df.set_axis(index, axis)`, `index` could be a `pd.Index` or `pd.MultiIndex`.

`df.reset_index(indexes, drop)`,
`drop` indicates whether drop or add to column, default `False`

`df.reindex(indexes)`, use new `indexes` and align based on index.
It is often used to resort index.\
`df_1.reindex_like(df_2)` is similar.

## Calculation between index

$$ \rm S_A.intersection(S_B) = \rm S_A \cap S_B \Leftrightarrow \rm \{x|x\in S_A\, and\, x\in S_B\} $$
$$\rm S_A.union(S_B) = \rm S_A \cup S_B \Leftrightarrow \rm \{x|x\in S_A\, or\, x\in S_B\}$$
$$\rm S_A.difference(S_B) = \rm S_A - S_B \Leftrightarrow \rm \{x|x\in S_A\, and\, x\notin S_B\}$$
$$\rm S_A.symmetric\_difference(S_B) = \rm S_A\triangle S_B\Leftrightarrow \rm \{x|x\in S_A\cup S_B - S_A\cap S_B\}$$

At first, we should use `unique` method to remove duplicates.