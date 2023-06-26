# Change shape
## Flatten

```python3
arr.flat  # a view
arr.flatten(order)
arr.ravel(order)

np.flatten(arr, order)
np.ravel(arr, order)
```
`order`, {'C', 'F', 'A', 'K'}, optional, default 'C'.
1. ‘C’, in row-major (C-style) order. 
2. ‘F’, in column-major (Fortran- style) order. 
3. ‘A’, in column-major order if `arr` is Fortran contiguous in memory, row-major order otherwise. 
4. ‘K’, in the order the elements occur in memory.

It is equivalent to
```python3
def flatten(arr, order="C") -> np.ndarray:
    if arr.ndim == 1:
        return arr
    match order:
        case 'F':
            return flatten(arr.T, order='C')
        case 'C':
            return np.concatenate([flatten(arr[i], order='C') for i in range(arr.shape[0])])
        case 'A':
            return flatten(arr, order='F') if arr.flags['C_CONTIGUOUS'] else flatten(arr, order='C')
        case 'K':
            return flatten(arr, order='C') if arr.flags['C_CONTIGUOUS'] else flatten(arr, order='F')
        case _:
            raise ValueError(f"order must be one of 'C', 'F', 'A', or 'K' (got '{order}')")
```

## Reshape
```python3
arr.reshape(*shape)  # or arr.reshape(shape), return a new array
arr.resize(shape, refcheck)  # reshape in place
np.resize(arr, size)
```

## Expand and squeeze
```python3
np.expand_dims(arr, expand_axis)
np.squeeze(arr)  # squeeze all dimensions with shape 1
np.squeeze(arr, squeeze_axis)
```

## Transpose
```python3
arr.T  # transpose
arr.transpose(axes) # faster
np.transpose(arr, axes) # slower
```

# Axis transform
## Move axis
```python3
np.moveaxis(arr, moved, target)
```
`moved`, list-like of dimension index, moved axis.\
`target`, list-like of dimension index, target axis.

## Swap axes
```python3
np.swapaxes(arr, axis1, axis2)
```
It swaps `axis1` and `axis2`.

# Dimension
## Dimension attributes
```python3
arr.shape
arr.ndim
```

## At least function
Transform `arr` to at least n dimensions.
```python3
np.atleast_1d(arr)
np.atleast_2d(arr)
np.atleast_3d(arr)
```

# Join and split
## Concat
```python3
np.concatenate(arrays, axis)
```
Concat `arrays` at `axis` direction. `axis` default 0.

## Split
```python3
np.split(arr, times, axis)
```
Split `arr` into `times` parts in `axis` direction.

## Stack
```python3
np.stack(arrays, axis)
```
Pile arrays at a **new** direction `axis`. `axis` default 0.

## Repeat
```python3
np.repeat(arr, times, axis)
```
Repeat `arr` `times` times one by one.\
If not assign `axis`, it will flatten `arr`.

## Block
```python3
np.block(arr_list)
```
`arr_list`, a structured list of array.

It is equivalent to
```python3
def block(arr_list: list) -> np.ndarray:
    if all(type(arr) is list for arr in arr_list): # continue unpacking
        return np.concatenate([block(l) for l in arr_list], axis=0)
    elif all(type(arr) is np.ndarray for arr in arr_list): # last layer
        return np.concatenate(arr_list, axis=-1) 
    else:
        raise ValueError("List depths are mismatched.")
```

## Tile
```python3
np.tile(arr, reps)
```
`reps`, the number of repetitions of `arr` along each axis.

It is equivalent to
```python3
def tile(arr: np.ndarray, reps: list) -> np.ndarray:
    res = np.copy(arr)
    for i, time in enumerate(reps[::-1]):
        if i < arr.ndim:
            res = np.concatenate([res] * time, axis=-i-1)
        else:
            res = np.stack([res] * time, axis=0)
    return res
```

# Delete and insert
```python3
np.delete(arr, deleted, axis)
np.insert(arr, index, inserted, axis)
np.append(arr, appended, axis)
```
If not assign `axis`, it will flatten `arr`.

```python3
np.trim_zeros(arr, trim)
```
`trim`, {'f', 'b', 'fb'}, default 'fb'.
1. 'f', delete front zeros
2. 'b', delete zeros at end

# Resort
## Flip
```python3
np.filp(arr, axes)
```
Flip `arr` in `axes` directions.

It is equivalent to
```python3
def flip(arr: np.ndarray, indices: list) -> np.ndarray:
    filp_slice = [slice(None, None, 1)] * arr.ndim
    for i in indices:
        filp_slice[i] = slice(None, None, -1)
    return arr[tuple(filp_slice)]
```

## Roll
```python3
np.roll(arr, shift, axes)
```
Roll `arr` `shift` steps in `axes` directions.\
If not assign `axes`, it will shift `arr` after flatten it, then reshape to origin.

## Rot90
```python3
np.rot90(arr, k, axes)
```
Rot `arr` from `axes[0]` to `axes[1]` `k` times.\
`axes` default `(0, 1)`

