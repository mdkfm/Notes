# object `str`
Object `str` is defined as a attribute of a `Seires` or a `Index`, 
specifically used to handle the textual content.
```python3
s.str
```

# Common method
```python3
s.str[n] # serial indexer
```

## Split
```python3
s.str.split(regex, n, expand)
s.str.rsplit(regex, n, expand)
```
`regex` is a regular expression as a seperator.\
`n` is the max num of split operations.\
`expand` is a bool value, indicating whether expands result as many columns.

## Merge
```python3
s.str.join(sep)
s1.str.cat(s2, sep, na_rep, join)
```
`sep` is a str as seperator.\
`na_rep` is a str to replace `NaN`.\
`join` is the method of joining.

## Match
```python3
s.str.contains(regex) # return bool value
s.str.startswith(regex)
s.str.endswith(regex)
s.str.find(string) # return index
s.str.rfind(string)
```

## Replace
```python3
s.str.replace(regex, value)
s.str.replace(regex, func)
s.str.replace(string, value, regex=False)
```
`regex` is a regular expression.\
`value` is the alternate value.\
`func`, inputs a `re.Match` object, outputs a string.

## Extract
```python3
s.str.extract(regex) # return a df
s.str.extractall(regex)
s.str.findall(regex) # return a series
```

## Letter processing
```python3
s.str.upper()
s.str.lower()
s.str.title()
s.str.capitalize()
s.str.swapcase()
```

## Numeric operation
```python3
pd.to_numeric(s, errors, downcast)
```
`s` is a `ps.Series`.\
`errors` is a str in ['raise', 'coerce', 'ignore'],
indicating how to process error.\
`downcast` is a str in ['integer', 'signed', 'unsigned', 'float'].

## Statistics
```python3
s.str.len()
s.str.count(regex)
```

## Formatting
```python3
s.str.strip()
s.str.rstrip()
s.str.lstrip()
s.str.pad(num, direction, padding)
```
`num` is the min length.\
`direction` is  a string in ['right', 'left', 'both'],
indicating the padding direction.\
