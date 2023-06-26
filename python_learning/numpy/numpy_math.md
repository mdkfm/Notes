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

# Set calculation
## Unique
```python3
arr.unique()
```

## include
```python3
np.in1d(arr1, arr2, assume_unique) # flatten
np.isin(arr1, arr2, assume_unique) # not flatten
```
`assume_unique`, 
if the value of`arr1` and `arr2` are unique, 
it could accelerate.

Consult if elements of `arr1` are in `arr2`, 
return a `np.ndarray` with same shape as `arr1`.

## Intersect
Get the intersection of `arr1` and `arr2`
```python3
np.intersect1d(arr1, arr2, assume_unique, return_indices)
```
`return_indices`, bool, if `True`, return a indices array, default `False`.\
Return a `np.ndarray` with one dimension.

## Union
```python3
np.union1d(arr1, arr2, assume_unique, return_indices)
```

## Difference
```python3
np.setdiff1d(arr1, arr2, assume_unique, return_indices)
```

## Exclusive OR
```python3
np.setxor1d(arr1, arr2, assume_unique, return_indices)
```

# Functions
## Trigonometric function
Trigonometric functions and their inverse functions.
```python3
np.sin(arr)
np.arcsin(arr)
```
Hyperbolic functions and their inverse functions.
```python3
np.sinh(arr)
np.arcsinh(arr)
```

These all above are `ufunc`.

Conversion between angle and radian.
```python3
np.deg2rad(arr)
np.rad2deg(arr)
```

Unwrap
```python3
np.unwrap(arr, discont, axis, period)
```
It will make the difference between any adjacent elements less than `discont`.

`discont`, the max discontinuous range, default `period / 2`.
`period`, process every element by plus or minus `period`.

## Exponent and logarithm
```python3
np.log(arr)
np.exp(arr)
np.expm1(arr) # np.exp(arr) - 1
np.log1p(arr) # np.log(arr + 1)
np.logaddexp(arr1, arr2)  # np.log(np.exp(arr1) + np.exp(arr2))
np.logaddexp2(arr1, arr2), np.log2(np.exp2(arr1) + np.exp2(arr2))
```

## Algebraic 
```python3
np.lcm(arr1, arr2)
np.gcd(arr1, arr2)
```

More refer to [Mathmatics functions](https://numpy.org/doc/stable/reference/routines.math.html)

## Automatic domain
When the data type of input and output are different, use `np.enath`.\
Support API
- `sqrt`, `power`
- `log`, `log2`, `log10`, `logn`
- `arccos`, `arcsin`, `arctan`


# Number calculate
## Round
```python3
np.around(arr, accuracy)
arr.round(accuracy)
np.fix(lst)
np.trunc(lst)
np.rint(lst)
np.floor(lst)
np.ceil(lst)
```
Beside `np.fix`, others are belong to `ufunc`.

## Sum, product and difference
```python3
np.sum(arr)
np.cumsum(arr)
np.product(arr)
np.cumproduct(arr)
```

```python3
np.diff(arr, times, append, axis)
```

## Signal
```python3
np.sign(arr)
np.heaviside(arr1, num)
```

## Clip
```python3
np.clip(arr, a_min, a_max)
```

## Interp
```python3
np.interp(x_inserted, x, y)
```
Example
```python3
import numpy as np
import matplotlib.pyplot as plt
x = np.linspace(0, 2*np.pi, 10)
y = np.sin(x)
xvals = np.linspace(0, 2*np.pi, 20)
yinterp = np.interp(xvals, x, y)
plt.plot(x, y, 'o')
plt.plot(xvals, yinterp, '-x')
plt.show()
```

# Gradient and integral
## Gradient
```python3
np.gradient(f, *varargs, axis, edge_order)
```
It calculates the gradient of `f`.

`f`, array_like. An N-dimensional array containing samples of a scalar function.

`varargs`, list of scalar or array, optional
Spacing between f values. Default unitary spacing for all dimensions. Spacing can be specified using:
1. single scalar to specify a sample distance for all dimensions. 
2. N scalars to specify a constant sample distance for each dimension. i.e. dx, dy, dz, … 
3. N arrays to specify the coordinates of the values along each dimension of F. \
The length of the array must match the size of the corresponding dimension 
4. Any combination of N scalars/arrays with the meaning of 2. and 3.

`edge_order`, {1, 2}, optional. The method to calculate the edge gradient.
More refer to ()[https://numpy.org/doc/stable/reference/generated/numpy.gradient.html#numpy-gradient]

## Integral
```python3
np.trapz(y, x, dx, axis)
```
`dx`, default 1.0, if there is no `x`, use `dx`.

It will use the trapezoidal rule to calculate integral.

# Polynomial
The API of `np.polynomial`
1. `Polynomial`
2. `Chebyshev`
3. `Hermite`, for Physicist
4. `HermiteE`, for Probabilist
5. `Laguerre`
6. `Legendre`

More refer to [Numpy Polynomial](https://numpy.org/doc/stable/reference/routines.polynomials.html)

Every kind of polynomials has its own term.
1. `Polynomial`, $x^n$
2. `Chebyshev`, $T_n(x) = \frac{z^n + z^{-n}}{2}, x = \frac{z + z^{-1}}{2}$
3. `Hermite`, for Physicist, $H_n(x) = (-1)^n e^{x^2} \frac{d^n}{dx^n} e^{-x^2}$
4. `HermiteE`, for Probabilist, $He_n(x) = (-1)^n e^{\frac{x^2}{2}} \frac{d^n}{dx^n} e^{\frac{-x^2}{2}}$
5. `Laguerre`, $L_n(x) = \frac{e^x}{n!} \frac{d^n}{dx^n} x^n e^{-x}$
6. `Legendre`, $P_n(x) = \frac{1}{2^n n!} \frac{d^n}{dx^n} |(x^2 - 1)^n|$

## Initialize
### From coefficient
```python3
from numpy.polynomial import Polynomial as P

P(coef, domain, window)
```
`coef`, list-like, `[a0, a1, ..., an]`. 
It determine a polynomial, $a_0 + a_1 x^1 + ... + a_n x^n$.

### From roots
```python3
P.fromroots(roots)
```

### From fit
```python3
P.fit(x, y, deg)
```
Return a polynomial 
that fits the function $f:x \rightarrow y$.\
`deg`, the degree of polynomial.

## Calculation
### Normal
Substituting a num into a polynomial
```python3
from numpy.polynomial import Polynomial as P

p1 = P(coef1)
p1(num) # Substituting num into p1
```

Get the roots of polynomials
```python3
p.roots()
```

### Calculation between polynomials
Two polynomials must have same `domain` and `window`


```python3
p2 = P(coef2)
p1 + p2 # return a new polynomial
p2 + p1.coef # equivalent to p1 + p2
```
`p.coef` is the coefficients list of `p`.\
Return a new polynomial.

```python3
p1 / p2
p1 % p2
divmod(p1, p2) # return (p1 / p2, p1 % p2)
```
It is same with partial factorization.
```python3
quotient, remainder = divmod(p1, p2)
p1 == quotient * p2 + remainder # True
```

### Integration
```python3
p.integ(m=time, k, lbnd)
```
`m`, int, the integration time.\
`k`, array-like, `[C_1, C_2, C_3, ..., C_m]`, 
the integration constants, `C_i` default 0.\
`lbnd`, The lower bound of the definite integral.

Example,
```python3
p.integ(m=1, k=[C], lbnd)
```
Result, $\int^{x}_{lbnd} p dx + C$

### Derive
```python3
p.derive(time)
```

## Convert 
```python3
p.convert(domain, window)
```
Change `p.domain` and `p.window`.

```python3
from numpy.polynomial import chebyshev as T
T.cast(p)
```
Convert `p` to another kind of polynomial.

## Print
```python3
np.polynomial.set_default_printstyle(style)

print(p)
print(f'{p:unicode}')
print(f'{p:ascii}')
```
`style`, str, {'unicode', 'ascii'}.


# Relation calculation
## Bool
```python3
np.all(arr, axis)
np.any(arr, axis)
```

## Value
- `isfinite`, is finite
- `isnan`, is not a num
- `isnat`, is not a time
- `isinf/isneginf/isposinf`, is infinite, negative infinite, positive infinite.

## Data type
- `iscomplex`, is complex num
- `iscomplexobj`, is complex obj
- `isfortran`, is F-Style
- `isreal`, is real num
- `isrealobj`, is real obj
- `isscalar`, is scalar

## Bool calculation
```python3
np.logical_or(arr1, arr2)
np.logical_and(arr1, arr2)
np.logical_xor(arr1, arr2)
```
These return bool values.

It is corresponding to
```python3
arr1 | arr2
arr1 & arr2
arr1 ^ arr2
```
When the data type of `arr1` and `arr2` are not all bool,
these returns 0 and 1 instead of `False` and `True`.


## Numeric compare
### CLose
```python3
np.allclose(arr1, arr2, atol, rtol, equal_nan)
np.isclose(arr1, arr2, atol, rtol, equal_nan)
```
It will test
$$
|arr1 - arr2| <= (\text{atol} + \text{rtol}  * |b|)
$$
`atol`, default 1e-08.\ 
`rtol`, default 1e-05.\
`equal_nan`, bool, whether two `np.nan` are equal or not, default `False`.

### Equal
```python3
np.array_equal(arr1, arr2, equal_nan)
np.array_equiv(arr1, arr2, equal_nan) # broadcast aat first
```

### Compare
```python3
np.greater(arr1, arr2)
arr1 > arr2
np.greater_equal(arr1, arr2)
arr1 >= arr2
np.less(arr1, arr2)
arr1 < arr2
np.less_equal(arr1, arr2)
arr1 <= arr2
np.equal(arr1, arr2)
arr1 == arr2
```

# Binary calculation
We should know the data type of array at first, then use binary calculations.

## Bool
```python3
np.bitwise_and(a, b)
np.bitwise_or(a, b)
np.bitwise_xor(a, b)

np.bitwise_not(a)
```

## Shift
```python3
np.left_shift(arr)
np.right_shift(arr)
```

## Pack and unpack
Pack array as bits and unpack.
```python3
np.packbits(arr)
np.unpackbits(arr)
```
