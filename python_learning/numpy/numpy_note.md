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
```

## Random
Random distribution
```python3
np.random.rand(size) # 0-1 uniform
np.random.random(shape) # 0-1 uniform
np.random.uniform(low, high, size) # uniform

np.random.randint(low, high, size) # discrete uniform
np.random.randn(*size) # standard normal
```

### Random number generator
Recommend using a random number generator,
```python3
rng = np.random.default_rng(seed)
rng.random(size) # 0-1 uniform
rng.uniform(low, high, size) # uniform

rng.integer(low, high, size) # discrete uniform
rng.standard_normal(size)
rng.normal(loc, scale, size)
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

# Ndarray attributes
## Size
```python3
arr.ndim
arr.shape
arr.size
```

# Change
## Change shape
```python3
np.expand_dim(arr, expand_axis)
np.squeeze(arr)  # squeeze all dimensions with shape 1
np.squeeze(arr, squeeze_axis)

arr.reshape(*shape)  # or arr.reshape(shape), return a new array
arr.resize(shape, refcheck)  # reshape in place
np.resize(arr, size)

arr.ravel()  # flatten
arr.T  # transpose

arr.transpose(axes) # faster
np.transpose(arr, axes) # slower
```

## Change elements
```python3
np.minimum(arr, max) # replace nums bigger than max with max
np.maximum(arr, min)
```

# Index
`np.ndarray` could use multidimensional slice and discrete slice.

# Join and Split
## Concat
```python3
np.concatenate(arrays, axis)
```
Concat some arrays at `axis` direction. `axis` default 0.

## Stack
```python3
np.stack(arrays, axis)
```
Pile arrays at a new direction `axis`. `axis` default 0.

## Repeat
```python3
np.repeat(arr, times, axis)
```
Repeat `arr` one dimension by one dimension.

## Split
```python3
np.split(arr, times, axis)
```

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

## Sample
Recommend,
```python3
rng = np.random.default_rng(seed)
rng.choice(a, size, replace, p)
```
`a`, {array_like, int}, 
corresponding choice from `a` or `np.arange(a)`.\
`replace`, bool, whether put elements back.\
`p`, probability list.

Old,
```python3
np.random.choice(a, size, replace, p)
```

## Sort
```python3
np.argmax(arr, axis) # return index
np.argmin(arr, axis)

np.argsort(arr, axis) # return all index after sort
```

