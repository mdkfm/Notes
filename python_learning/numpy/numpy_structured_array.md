# Initialization
```python3
np.array(data, dtype)
np.rec.array(data, dtype) # this method will register column names as attributes
```
`data`, list-like, with tuple elements. \
`dtype`, list-like, [(column_name, data_type), ...],  defines the structure of tuples.

Example,
```python3
# structured
np.array(
    [('Rex', 9, 81.0), ('Fido', 3, 27.0)],
    dtype=[('name', '(5, 3)U10'), ('age', 'i4'), ('weight', 'f4')]
) # shape: (2, )

# not structured
np.array([('Rex', 9, 81.0), ('Fido', 3, 27.0)]) # shape: (2, 3)
```

