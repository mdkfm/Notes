# Universal function
Universal function operates elements in arrays one by one, 
supporting array broadcasting, type conversion, and so on.

Such as, `np.add`, `np.multiply`, etc.
```python3
isinstance(np.add, np.ufunc)
isinstance(np.multiply, np.ufunc)
```
Consult info of `np.ufunc`
```python3
dir(np.ufunc)
np.info(np.ufunc)
```

## Parameters
Shared parameters:
1. `dtype`, output datatype.
2. `out`, output address
3. `where`, a bool list-like, whether element store. 
```python3
np.add(x1, x2, dtyep, out=x3, where=[True] * x1.shape[0])
```

# Custom class 
use magic method `__array_ufun__` to customize universal func
```python3
class MyArray(np.lib.mixins.NDArrayOperatorsMixin):

    def __init__(self, lst: list):
        self.list = lst

    def __array_ufunc__(self, ufunc, method, *inputs, **kwargs):
        return ufunc(np.array(self.list), inputs[1])
```

# Method
Every universal function is a instance of class `np.ufunc`.
It has some useful method:
1. `accumulate`  --  accumulate(array, axis=0, dtype=None, out=None)
2. `at`  --  at(a, indices, b=None, /)
3. `outer`  --  outer(A, B, /, **kwargs)
4. `reduce`  --  reduce(array, axis=0, dtype=None, out=None, keepdims=False, initial=<no value>, where=True)
5. `reduceat`  --  reduceat(array, indices, axis=0, dtype=None, out=None)

## `reduce`
Operate along the selected direction, return a aggregation array.
```python3
np.add.reduce(array, axis=0, dtype=None, out=None, keepdims=False, initial=<no value>, where=True)
```
`keepdims`, bool, whether keep the num of dimensions.\
`initial`, initial value.\

## `accumulate`
Accumulation of all elements along selected direction.
```python3
np.add.accumulate(array, axis=0, dtype=None, out=None)
```

## `reduceat`
Operate along the selected direction, according to indices.
```python3
np.add.reduceat(array, indices, axis=0, dtype=None, out=None)
```
For i in range(len(indices)), `reduceat`
computes `ufunc.reduce(array[indices[i]:indices[i+1]])`, 
which becomes the i-th generalized “row” parallel to axis in the final result. 
There are three exceptions to this:
1. when `i = len(indices) - 1` (for the last index), `indices[i+1] = array.shape[axis]`.
2. if `indices[i] >= indices[i + 1]`, the i-th generalized “row” is simply `array[indices[i]]`.
3. if `indices[i] >= len(array)` or `indices[i] < 0`, raise error.

## `outer`
```python3
np.add.outer(arr1, arr2)
```
Passed two array, it is equivalent to
```python
def outer(arr1, arr2, op):
    arr1, arr2 = np.array(arr1), np.array(arr2)
    dim1, dim2 = len(arr1.shape), len(arr2.shape)
    arr1 = np.expand_dims(arr1, tuple(i + dim1 for i in range(dim2)))
    arr2 = np.expand_dims(arr2, tuple(i for i in range(dim1)))
    return op(arr1, arr2)
```
Operate every couple elements, return a result array. 

## `at`
```python3
np.add.at(arr1, indices, arr2)
```
Operate `arr1` in situ, the second operand is `arr2`, return `None`.\
It is equivalent to
```python3
def at(arr1, indices, arr2, op):
    arr1[indices] = op(arr1[indices], arr2)
    return None
```