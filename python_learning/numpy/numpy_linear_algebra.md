# Array product
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
np.dot(a, b) == np.tensordot(a, b, axes=(-1, -2))


np.dot(a, b)[i, ..., j, u, ..., v, m]
== np.sum(a[i, ..., j, :] * b[u, ..., v, :, m])
```
For more detail of `np.dot`, refer to [numpy.dot](https://numpy.org/doc/stable/reference/generated/numpy.dot.html#numpy.dot).\

## Vdot
```python3
np.vdot(a, b) # np.dot(a.flatten(), b.flatten())
```

## Matmul
```python3
np.matmul(a, b)
arr1 @ arr2
```
This is a `ufunc`, but `dot` is not.
When `a.ndim <= 2 and b.ndim <= 2`, this is normal matmul.

When `a.ndim > 2 and b.ndim > 2`, 
the last two dimensions are regarded as a matrix.\
Then `a` and `b` could be regard as two arrays filled with matrix elements.\
Broadcast at first, then calculate the matmul product of matched elements.\
So, we need
1. `a.shape[:-2]` and `b.shape[:-2]` are matched
2. `a.shape[-1] == b.shape[-2]`, matmul needs

When `a.shape[:-2] == b.shape[:-2]`
```python3
np.matmul(a, b)[i, ..., j]
== np.matmul(a[i, ..., j], b[i, ..., j]) # two equal matrices 
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


## Cross
```python3
np.cross(a, b, axisa, axisb, axisc, axis) # return c
```
`axisa` : int,
Axis of `a` that defines the vector(s), default -1.\
`axisb` : int,
Axis of `b` that defines the vector(s), default -1.\
`axisc` : int,
Axis of `c` containing the cross product vector(s).  
Ignored if both input vectors have dimension 2, as the return is scalar, default -1.\
`axis` : int,
If defined, the axis of `a`, `b` and `c` that defines the vector(s) and cross product(s). 
Overrides `axisa`, `axisb` and `axisc`.\

## Outer
```python3
np.outer(a, b)
```
It is equal to
```python3
a.flatten().reshape(-1, 1) @ b.flatten().reshape(1, -1)
```

## Kronecker
For two dimensions,
$$
A\otimes B={\begin{bmatrix}a_{{11}}B&\cdots &a_{{1n}}B\\\vdots &\ddots &\vdots \\a_{{m1}}B&\cdots &a_{{mn}}B\end{bmatrix}}.
$$
```python3
np.kron(a, b)
```
At first, align the dimensions of `a` and `b`.\

When `a.ndim == b.ndim`, 
it returns a array with shape `a.shape * b.shape`

```python3
import numpy as np

n = a.ndim
axes1 = [2 * i for i in range(1, n + 1)]
axes2 = [2 * i for i in range(0, n)]
a_mid = np.expand_dims(a, axis=axes1)
b_mid = np.expand_dims(b, axis==axes2)
shape = np.multiply(a.shape, b.shape)

np.array_equal(
    np.kron(a, b),
    (a_mid * b_mid).reshape(shape)  # True
)
```

## Multi-dot
This is a tool to calculate the `dot` product of a series of arrays. 
```python3
np.linalg.multi_dot(arrays)
```
It could find a good path to calculate.



# Matrix
## Norm
```python3
np.linalg(a, ord, axis, keepdim)
```
`ord`, str, the norm kind.

For a matrix,

| ord    | norm for matrices            |           norm for vectors |                           detail |
|:-------|:-----------------------------|---------------------------:|---------------------------------:|
| None   | Frobenius norm               |                     2-norm |          `np.sqrt(np.sum(a**2))` |
| 'fro'  | Frobenius norm               |                         -- |          `np.sqrt(np.sum(a**2))` |
| 'nuc'  | nuclear norm                 |                         -- |           `np.sum(LA.svd(a)[1])` | 
| inf    | max(sum(abs(x), axis=1))     |                max(abs(x)) | `np.max(np.sum(abs(a), axis=1))` |
| -inf   | min(sum(abs(x), axis=1))     |                min(abs(x)) | `np.min(np.sum(abs(a), axis=1))` |
| 0      | --                           |                sum(x != 0) | `np.max(np.sum(abs(a), axis=0))` |
| 1      | max(sum(abs(x), axis=0))     |                   as below | `np.max(np.sum(abs(a), axis=0))` |
| -1     | min(sum(abs(x), axis=0))     |                   as below | `np.min(np.sum(abs(a), axis=0))` |
| 2      | 2-norm (largest sing. value) |                   as below |           `np.max(LA.svd(a)[1])` |
| -2     | smallest singular value      |                   as below |           `np.min(LA.svd(a)[1])` |
| other  | --                           | sum(abs(x)**ord)**(1./ord) |                                  |


`axis`, {None, int, 2-tuple of ints}, default `None`
1. int, it specifies the axis of `a` along which to compute the vector norms.  
2. 2-tuple, it specifies the axes that hold 2-D matrices.
3. None, either a vector norm (when `a`is 1-D) or a matrix norm (when `a` is 2-D) is returned.

## Trace
```python3
np.tarce(a)
```

## Eigen value and vector
`a` could be a matrix or a array of matrices.
```python3
np.linalg.eig(a) # return the eigen values and vectors
np.linalg.eigvalues(a)
```
We have
```python3
w, v = np.linalg.eig(a)

np.allclose(a @ v, np.expand_dims(w, axis=[-2]) * v) # True
```

For Hermitian matrix, we have
```python3
np.linalg.eigh(a)
np.linalg.eigvals(a)
```

## Equation
We can solve the simple equation
$$ ax = b $$

### `np.linalg.solve`
The operator is matmul.\
`a` is a array of square matrices, `b` is a array of matrices or vectors
```python3
np.linalg.solve(a, b)
```
Two situations:
1. `b.ndim == a.ndim`, the last two dimensions are regarded as matrices.
2. `b.ndim == a.ndim - 1`, 
the last two dimensions of `a` are regarded as matrices, 
the last dimensions of `b` is regarded as column vectors.

Broadcast `a` and `b` as arrays of matrices or vectors, then calculate the result `x`.\
The matrices in `a` should be square, 
the matrices or vectors in `b` should be matched with matrices in `a`.

We can check out the result.
```python3
x = np.linalg.solve(a, b)

np.allclose(a @ x, b) # b.ndim == a.ndim
np.allclose((a @ np.expand_dims(x, axis=-1)).squeeze(axis=-1), b) # b.ndim == a.ndim - 1 
```

### `np.linalg.tensorsolve`
The operator is `tensordot`.
```python3
np.linalg.tensorsolve(a, b)
```
Condition:
1. `a.shape == b.shape + Q`
2. `prod(Q) == prod(b.shape)`

It means that `a` is a kind of 'square'.\
The result `x.shape == Q`.

We can check the result
```python3
x = np.linalg.solve(a, b)

np.allclose(np.tensordot(a, x, axes=b.ndim+1), b) # True
```

## Determinant
```python3
np.linalg.det(a)
```

## Inverse

### For square
```python3
np.linalg.inv(a)
```
Check, when `a` is a square
```python3
inva = np.linalg.inv(a)

np.allclose(a @ inva, np.eye(a.shape[0])) # True
```

### For normal
```python3
np.linalg.pinv(a)
```
Check, when `a` is a normal square
```python3
inva = np.linalg.pinv(a)

np.allclose(a @ inva, np.eye(min(a.shape))) # True
```

### For `tensordot`
```python3
np.linalg.tensorinv(a, ind)
```
`ind`, int, 
number of first indices that are involved in the inverse sum, default 2.\
`a`, `prod(a.shape[:ind]) == prod(a.shape[ind:])`

Check,
```python3
inva = np.linalg.tensorinv(a, ind=ind)

n = a.ndim - ind
shape = a.shape[:ind]
eye = np.eye(np.prod(shape)).reshape(shape * 2)
np.allclose(np.tensordot(a, inva, axes=n), eye) # True
```

## Decompose
### Cholesky decomposition
```python3
ca = np.linalg.cholesky(a)

np.array_equil(ca @ ca.T, a) # True 
```
`a`, symmetric positive definite matrix, 
and all feature values must be greater than zero.

### QR decomposition
```python3
q, r = np.linalg.qr(a) 
# r is a upper triangular matrix, q is a orthogonal matrix
qt = np.transpose(q, axes=list(range(q.ndim - 2)) + [-1, -2]) 
np.allclose(q @ qt, np.eye(q.shape[-1]))

np.allclose(q @ r, a)
```

### SVD
```python3
u, s, vh = np.linalg.svd(a)
```
`u` and `vh` are unitary matrices.\
`s` is a array of singular values with one dimension.


## Einsum
```python3
np.einsum(subscripts, *operands)
```
`subscripts`, str, 
the subscripts string is a comma-separated list of subscript labels, 
where each label refers to a dimension of the corresponding operand.\
If a label is repeated, it is summed, else not summed.\

In implicit mode, 
the chosen subscripts are important since the axes of the output are reordered alphabetically.
```python3
np.array_equal(
    np.einsum('ij, jk', a, b),
    a @ b
)

np.array_equal(
    np.einsum('ij, jh', a, b),
    (a @ b).T
)
```

In explicit mode 
the output can be directly controlled by specifying output subscript labels.\
This requires the identifier ‘->’ as well as the list of output subscript labels.
```python3
np.array_equial(
    np.einsum('ij,jk->ik', a, b),
    np.einsum('ij,jh->ih', a, b)
)
```

To enable and control broadcasting, use an ellipsis.
```python3
np.array_equal(
    np.einsum('...i, i', a, b),
    np.sum(b * a, axis=1)
)

np.array_equal(
    np.einsum('i..., i', a, b),
    np.sum(b * a.reshape(-1, 1), axis=0)
)
```

## Pad
```python3
np.pad(array, 
       pad_width, 
       mode, 
       stat_length, 
       constant_values, 
       end_values, 
       reflect_type)
```
`mode`, {'edge', 'linear_ramp', 
'maximum', 'mean', 
'median', 'minimum', 
'reflect', 'symmetric', 
'wrap', 'empty'}, 
more refer to [np.pad](https://numpy.org/doc/stable/reference/generated/numpy.pad.html#numpy.pad)\

## Convolve
```python3
np.convolve(a, v, mode)
```
`mode`, {'full', 'valid', 'same'}, default 'full'.
