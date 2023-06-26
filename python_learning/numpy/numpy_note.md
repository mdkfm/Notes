# Generate
## Normal
```python3
np.array(array)
np.arange(start, end, step)
np.linspace(start, end, num)
np.logspace(start, end, num, base)
```

## All 1/0,
```python3
np.ones(size) # default float
np.ones_like(ndarray)
np.zeros(size) # default float
np.zeros_like(ndarray)
np.eye(n, offset) # Diagonal matrix
```

## Full
```python3
np.full(shape, num) # full of num
```

# Bool
```python3
np.alltrue(ndarray)
ndarray.all()
ndarray.any()
```

# Read and save
```python3
np.save(file, array)
np.savez(file, *arrays)
np.savez_compressed(file, *arrays)

np.load(file)
```

# Index
`np.ndarray` could use multidimensional slice and discrete slice.


# Filter
## Filter
```python3
np.where(condition) # return index of `True`
np.where(condition, arr, replace)
```

## Extract
```python3
np.extract(condtion, arr) # return a array with one dimension
np.unique(arr)
```






