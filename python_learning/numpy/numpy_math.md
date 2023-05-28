[toc]

# Constant
## Normal 
```python3
np.e  # 自然对数
np.pi  # PI
np.PZERO  # 0
np.NZERO  # -0
```

## Special
```python3
np.newaxis  # None
np.nan  # 空值, float
np.inf  # infinite
np.NINF # negative infinite
```

Judge
```python3
np.isnan(arr)
np.isinf(arr)
np.isposinf(arr)
np.isneginf(arr)
np.isfinite(arr)
```

# Normal function
More refer to [Mathematical functions](https://numpy.org/doc/stable/reference/routines.math.html)
```python3
np.log(arr)

np.round(arr, digit)
np.floor(arr)
np.ceil(arr)

np.mod(arr, divisor)
```

# Statistics
Usual parameters `axis, keepdim`.\
`np.ndarray` methods, `max, min`.\
`np` methods, passed `arr`,
```python3
np.amax(arr)
np.amin(arr)
np.median(arr)
np.quantile(arr, q)
np.average(arr)
np.sum(arr)
np.cumsum(arr)
np.std(arr)
np.var(arr)
```

# Matrix
## Dot
```python3
np.dot(a, b)
a.dot(b)
```
Condition: 
1. `b.ndim` is 1, condition is `a.shape[-1] == b.shape[-1]`
2. other, `a.shape[-1] == b.shape[-2]`

Out: `out.shape` is `(*a.shape[:-1], *b.shape[:-2], b[-1])` 
```python3
np.dot(a, b)[i, ..., j, u, ..., v, m] \
== np.sum(a[i, ..., j, :] * b[u, ..., v :, m])
```
For more detail of `np.dot`, refer to [numpy.dot](https://numpy.org/doc/stable/reference/generated/numpy.dot.html#numpy.dot).\



## Matmul
```python3
np.matmul(a, b)
arr1 @ arr2
```

## Vdot
```python3
np.vdot(a, b) # np.sum(a * b)
```

## Inner
```python3
np.inner(a, b)
```
Condition: `a.shape[-1]` == `b.shape[-1]`.\
Out: `out.shape` is `(*a.shape[:-1], *b.shape[:-1])`
```python3
np.inner(a, b) == np.tensordot(a, b, axes=(-1,-1)) # True

np.inner(a, b)[i, ..., j, u, ..., v] \
== np.sum(a[i, ..., j, :] * b[u, ..., v, :]) # True
```

## Determinant
```python3
np.linalg.det(a)
```

## Inverse Matrix
```python3
np.linalg.inv(a)
```