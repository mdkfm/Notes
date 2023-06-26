# Str
All API are under `np.char`\
Point at two data types.
```python3
np.str_, np.unicode_, np.str0 # np.str_

np.bytes_, np.string_ # np.bytes_
```

## Calculation
```python3
np.char.add(arr1, arr2)
np.char.multiply(arr, time) # when time less than 0, set it as 0
```

## String process
- `capitalize`
- `title`
- `center`, center fill.
- `ljust/rjust`, left or right fill
- `zfill`, 0 left fill
- `decode/encode`
- `expandtabs`, replace tab as blank
- `join`
- `lower/upper`
- `swapcase`, swap lower and upper
- `lstrip/rstrip/strip`, strip
- `replace`
- `translate`
- `partition/rpatition`, left or right three partition
- `split/splitlines`, split


### Fill
```python3
np.char.center(arr, length, filled)
np.char.ljust(arr, length, filled)
np.char.rjust(arr, length, filled)
np.zfill(arr, length)
```

### Encode and decode
```python3
np.char.encode(arr, encoding)
np.char.decode(arr, encoding)
```

### Replace
```python3
np.char.expandtabs(arr, tabsize)
np.char.lower(arr)
np.char.upper(arr)
np.char.swapcase(arr)
np.char.strip(arr)
```

```python3
np.char.replace(arr, replaced, value, time)
```
`time`, int, the max replace time.

```python3
np.char.translate(arr, table, deletechars)
```
It will delete `deletechars` in `arr` at first.\
The remaining characters have been mapped through the given translation `table`.\
`arr`, array-like of str or unicode.\
`table`, str of length 256.

### Join
```python3
np.char.join(sep, arr)
```

### Split
```python3
np.char.partition(arr, sep)
np.char.rpartition(arr, sep)
np.char.split(arr, sep)
np.char.splitlines(arr) # np.char.split(arr, sep='\n')
```

## Compare
```python3
np.char.greater(arr1, arr2)
arr1 > arr2
np.char.greater_equal(arr1, arr2)
arr1 >= arr2
np.char.less(arr1, arr2)
arr1 < arr2
np.char.less_equal(arr1, arr2)
arr1 <= arr2
np.char.equal(arr1, arr2)
arr1 == arr2
```

## Statistics method
```python3
np.char.count(arr, counted, start, end)
```
It counts `counted` in arr.

```python3
np.char.str_len(arr)
```
Return the length of str in `arr`.

```python3
np.char.find(arr, target, start, end)
```
If not find, return -1.

```python3
np.char.index(arr, target)
np.char.rindex(arr, target)
```
Search `target` in `arr` from left to right or from right to left,\
then return the index.\
If not find, raise error.

```python3
np.char.startswith(arr, target, start, end)
np.char.endswith(arr, target, start, end)
```

```python3
np.char.isspace(arr)
np.char.islower(arr)
np.char.isupper(arr)
np.char.istitle(arr)

np.char.isalpha(lst) # all letters
np.char.isalnum(lst) # all letters or nums
np.char.isdecimal(lst) # all decimal
np.char.isdigit(lst) # all digit
np.char.isnumeric(lst) # all numeric
```
[string - What's the difference between str.isdigit, isnumeric and isdecimal in python? - Stack Overflow](https://stackoverflow.com/questions/44891070/whats-the-difference-between-str-isdigit-isnumeric-and-isdecimal-in-python)

