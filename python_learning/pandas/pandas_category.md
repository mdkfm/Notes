[toc]

# Datatype `category`
```python3
s.astype('category')
```

Datatype `category` has a `cat` object, 
which has many useful attributes.
```python3
s.cat.categories # a index
s.cat.ordered # bool indicating order
s.cat.codes # a series of categories code
```

## Change
```python3
s.cat.add_categories(categories)
s.cat.remove_categories(categories)
s.cat.set_categories(categories) # set new categories, old set `NaN`
s.cat.remove_unused_categories()
s.cat.rename_categories(dict[category: new_name])
```
`categories` is a str or list.

## Ordered categories
```python3
s.cat.reorder_categories(oreder, ordered=True) # if not s.cat.ordered, set `ordered=True` 
s.cat.as_oredered()
s.cat.as_unordered()
```

# Interval

## Cut
```python3
pd.cut(s, bins, right, labels, retbins)
```
`bins`, int, sequence of scalars, or IntervalIndex. The criteria to bin by.\
`right`, bool, default True, indicating whether right closed.\
`labels`, list[str], default None, specifying the labels for the returned bins.\
`retbins`, bool, default False, whether to return the bins or not.

```python3
pd.qcut(s, q, labels, retbins) # quantile cut
```
`q`, int as number of quantiles, or list-like of float as quantile.

## Interval object

### Construction
```python3
pd.Interval(left, right, closed)
```
`left` is the left endpoint. `right` is the right endpoint.\
`closed` is a str in ['right', 'left', 'both', 'neither'].

### Attributes
Normal attributes, besides `mid, length, right, left, closed`, 
```python3
num in interval
interval1.overlap(interval2)
```
## IntervalIndex object
`pd.IntervalIndex` is the subclass of `pd.Index`.
```python3
issubclass(pd.IntervalIndex, pd.Index) # True
```

### Construction
Constructed from:
```python3
pd.IntervalIndex.from_breaks(breaks, closed)
pd.IntervalIndex.from_arrays(left, right, closed)
pd.IntervalIndex.from_tuples(tuples, closed)
```
From arithmetic sequence:
```python3
# `end` = `start` + `periods` * `freq`
pd.interval_range(start, end, periods, closed)
pd.interval_range(end, periods, freq, closed)
```
From `pd.Interval`:
```python3
pd.IntervalIndex(intervals, closed)
```

### Attributes
Normal attributes, besides `mid, length, right, left, closed`,
```python3
interval_index.contains(num)
interval_index.overlap(interval)
```