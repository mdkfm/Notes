# Equality Test
## Compare num
```python3
np.testing.assert_equal(arr1, arr2, message)
```
Compare corresponding elements in `arr1` and `arr2`.

```python3
np.testing.assert_equal(num, arr, message)
np.testing.assert_equal(arr, num, message)
```
Compare `num` with elements in `arr`.

```python3
np.testing.assert_array_equal(arr1, arr2, message)
```

## Compare string
```python3
np.testing.assert_string_equal(string1, string2)
```

# Close Test
```python3
np.testing.assert_allclose(num, expected, rtol, atol, equal_nan, err_msg)
```
If `abs(num - expected) < atol + rtol * abs(expected)`, it is close.\
`equal_nan`, whether two `np.nan` are close, default `True`.\

```python3
np.testing.assert_array_almost_equal_nulp(x, y, nulps)
```
`x` and `y`, num or list-like.\
`nulps`, int, the num of units in the last place.\
Test whether `abs(x-y) <= nulps * spacing(max(abs(x), abs(y)))`

```python3
np.testing.assert_array_max_ulp(x, y, maxulp)
```
Return:
Array 
containing number of 
representable floating point numbers 
between items in `x` and `y`.\
Raise:
AssertionError.
If one or more elements differ by more than `maxulp`.




# Less Test
```python3
np.testing.assert_array_less(x, y)
```
`x` and `y`, array_like.\
Raise AssertionError, 
if one or more elements in `x` 
are bigger than corresponding elements in `y`.

# Exception
Exception:
- `assert_raises`
- `assert_raises_regex`
- `assert_warns`

These could be used as context managers.

```python3
with np.testing.assert_raises(expected_error):
    ...
```
Raise AssertionError,
unless an exception of class `expected_error` is thrown.

```python3
with np.testing.assert_raises_regex(expected_error, expected_regex):
    ...
```
Raise AssertionError,
unless an exception of class `exception_error` and with message that matches `expected_regexp` is thrown.

```python3
 with np.testing.assert_warns(warning_class):
    ...
```
Raise AssertionError,
unless the specified warning is thrown.

More about warnings refer to [warnings — Warning control](https://docs.python.org/3/library/warnings.html).