# Mask module
`numpy.ma` is the module concluding all mask tools.
```python3
from numpy import ma
```

# Generate
```python3
ma.MaskedArray(a, mask=mask)
ma.array(a, mask=mask)
ma.masked_array(a, mask)

a.view(ma.MaskedArray)

ma.masked_object(a, masked)
ma.masked_where(condition, a)
```
More parameters:
1. `hard_mask`, bool, whether variable or not.
2. `fill_value`, default value for method `m.filled()`

# Attributes
```python3
m = ma.masked_where(condition, a)

m.data # return a
m.musk # return condition, a array of bools
m.fill_value
```

# Constant
```python3
ma.masked
```
The masked constant is a special case of MaskedArray, with a float datatype and a null shape.

```python3
ma.nomask
```
Value indicating that a masked array has no invalid entry.\ 
`nomask` is used internally to speed up computations when the mask is not needed.\
It is represented internally as `np.False_`.

```python3
ma.masked_print_option
```
String used in lieu of missing data when a masked array is printed. 
Default '--'.\
We could change it,
```python3
ma.masked_print_option.set_diplay(string)
```

# Change
## Unmask
Set a value to unmask.
```python3
m = ma.masked_where([0, 1], [1, 1])
m[1] = 1
```
For hard mask, we make it soft at first.
```python3
m = ma.masked_where([0, 1], [1, 1], hard_mask=True)
m.soften_mask()
m[1] = 1
```
Correspondingly, we could harden a soft mask.
```python3
m = ma.masked_where([0, 1], [1, 1])
m.harden_mask()
m[1] = 1 # not make a difference
```

Unmask all mask.
```python3
m.mask = ma.nomask
```

## Fill
```python3
m.filled(value)
```
`value`, the filled value, default `m.fill_value`.

# Ufunc
Module `numpy.ma` has many `ufunc`.

Example,
```python3
ma.log([-1, 0, 1, 2, 3, 4])
```
For in invalid or masked data, these would be masked in result.\
Return a masked array.

