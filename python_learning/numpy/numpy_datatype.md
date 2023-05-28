[toc]

# Overview

| Type               | Class                                                               | Note              |
|:-------------------|:--------------------------------------------------------------------|:------------------|
| bool               | `bool8`, `bool_`                                                    | not int           |
| int                | `int8/byte`, `int16/short`,<br/> `int32`, `int64/longlong`, `int_`  | \                 |
| uint               | `unsigned`                                                          | corresponding int |
| float              | `float16/half`, `float32/single`,<br/> `float64/double`, `float_`   | \                 |
| complex            | `complex64`, `complex128`, `complex_`                               | complex num       |
| str                | `str0`, `str_`                                                      | denoting unicode  |
| bytes              | `bytes_`, `string_`                                                 | \                 |
| datetime/timedelta | \                                                                   | \                 |
| structured array   | \                                                                   | \                 |

Underlined types are Python's, 
numpy can automatically convert Python's types to numpy's.
Following numbers indicate bits.

Relation between data types:

![](https://numpy.org/devdocs/_images/dtype-hierarchy.png)

origin: [Scalars — NumPy Manual](https://numpy.org/doc/stable/reference/arrays.scalars.html)

We could use `issubclass` to exam it, such as
```python3
issubclass(np.str_, np.flexible)
```

# Alias
Aliases of data types, used as parameters

| Format  | C Type       | Python Type   | Standard Size   |
|:--------|:-------------|:--------------|:----------------|
| `?`     | `_Bool`      | `bool`        | 1               |
| `b/B`   | `char`       | `int`         | 1               |
| `h/H`   | `short`      | `int`         | 2               |
| `i/I`   | `int`        | `int`         | 4               |
| `l/L`   | `long`       | `int`         | 4               |
| `q/Q`   | `long long`  | `int`         | 8               |
| `e`     | `half`       | `float`       | 2               |
| `f`     | `float`      | `float`       | 4               |
| `d`     | `double`     | `float`       | 8               |
More refer to [Python data type alias](https://docs.python.org/3/library/struct.html)

In numpy, we have more
- `c`：复数浮点
- `m/M`: timedelta / datetime
- `O`: Python 对象
- `U`: Unicode 字符串
- `V`: void
- `S/a`: 零终止字节（不推荐）


# Consult
Use follow method to consult info of types.
```python3
np.iinfo(np.int_) # int info
np.finfo(np.float64) # float info

np.info(obj) # also used to consult function
```

# Byte order (Endian)
Two endian: little-endian and big-endian.

![](https://qnimg.lovevivian.cn/cs-endian-1.jpg)

Picture origin: [Endianness - Wikipedia](https://en.wikipedia.org/wiki/Endianness)

Normally, we use little-endian.

Alias:

| Character | Byte order             | Size     | Alignment   |
|:----------|:-----------------------|:---------|:------------|
| =         | native                 | standard | none        |
| <         | little-endian          | standard | none        |
| \>        | big-endian             | standard | none        |
| !         | network (= big-endian) | standard | none        |

Consult byte order
```python3
# default =, same as <
np.dtype(np.int32).byteorder # result: =
np.dtype("<i").byteorder # =
np.dtype(">i").byteorder # >
```
