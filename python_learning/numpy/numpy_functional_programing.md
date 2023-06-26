[toc]

# Apply
```python3
np.apply_along_axis(func, axis, arr)
```
Apply the `func` along `axis`.\
`func`, input: a array (a part of `arr`); 
output: a value or an array.

```python3
np.apply_along_axis(func, arr, axes)
```
Apply the `func` along axis in `axes` iteratively.\   
`func`, input: `arr`, axis; 
output: an array with same shape as `arr`.


# Vectorize
## `vectorize`
```python3
np.vectorize(func, otypes, excluded, signature)
```
Transfer `func` into a vectorized function.\
`otypes`, datatype of output.
If `otypes` not assigned, it will call `func` to determine.\
`excluded`, the variables not to be vectorized.\
`signature`, the signature of vectorization. More refer to [numpy.ufunc.signature](https://numpy.org/doc/stable/reference/generated/numpy.ufunc.signature.html)

## `frompyfunc`
```python3
np.frompyfunc(func, nin, nout)
```
`nin`, the num of inputs.\
`nout`, the num of outputs.

## `piecewise`
Apply different `funcs` piecewise `arr`. 
```python3
np.piecewise(arr, conditions, funcs, **kw)
```
Every condition in `conditions` corresponds to a func in `funcs`.\
`kw`, other keyword args passed to func in `funcs`.
