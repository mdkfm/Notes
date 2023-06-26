# Compare
```python3
np.maximum(arr1, arr2)
np.minimum(arr1, arr2)

np.fmax(arr1, arr2)
np.fmin(arr1, arr2)

np.amax(arr1, arr2, axis)
np.amin(arr1, arr2, axis)

np.nanmax(arr1, arr2, axis)
np.nanmin(arr1, arr2, axis)
```
Compare `arr1` with `arr2`.\
Different
- 'maximum': comparing two arrays element by element
- 'fmax': Same as above, but missing values are ignored
- 'amax': along a given dimension
- 'nanmax': Same as above, but missing values are ignored

# Search
## Extreme Search
```python3
np.argmax(arr, axis) # return index of max num in axis
np.argmin(arr, axis) 
np.argsort(arr, axis) # return all index after sort
```
Return a `np.ndarray`, `nan` at first.

```python3
np.nanargmax(arr, axis)
np.nanargmin(arr, axis)
```
Ignore `nan`.

## Condition Search
### Search where
```python3
np.where(condition) 
np.where(condition, arr, replace)
```
`condition`, `arr`, `replace`, list-like or `np.ndarray`.

If only passed `condition`, return a indexes tuple 
of the elements that is not 0 or not `False`.

If passed `arr` and `replace`, 
replace elements in `arr` with `replace` at indexes above
return the result.

```python3
np.argwhere(condition)
```
It is similar to `np.where(condition)`, but returns a `np.ndarray`.

### Search to insert
```python3
np.searchsorted(arr, inserted, method, sorter)
```
`arr` should be sorted, or `sorter` is passed which give a sorted indexes.\
`inserted` could be a value or list-like.\
`method`, {'left', 'right'}, whether insert at left or right when meet two equal elements.\

Return a num or `np.ndarray`, up to `inserted`.

### Other
```python3
np.nonzero(arr) # same as np.where(arr)
np.flatnonzero(arr) # np.nonzero(arr) after flatten arr
```

# Sort
## Sort
```python3
arr.sort(axis, kind, order)
np.sort(arr, axis, kind, order)
```
`axis`, the sort direction, default -1.\
`kind`, the sort algorithm, 
{'quicksort', 'mergesort', 'heapsort', 'stable'}, default 'quicksort'.\
`order`, the field of `arr` used to sort.

Return the sorted array.

## Lexsort
```python3
np.lexsort(arrays, axis)
```
`arrays` should have same shapes.\
It sorts the subsequent arrays from back to front, 
and return an indices.

## Sort Complex
```python3
np.sort_complex(arr) # Sort real part then sort imaginary part
```

## Partition
```python3
np.partition(arr, kth, axis, kind, order)
np.argpartition(arr, kth, axis, kind, order) # return the indices
```
It will determine the `kth`th element after sorted, 
elements before are smaller, elements behind are greater.