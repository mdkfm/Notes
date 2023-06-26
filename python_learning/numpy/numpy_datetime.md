# Overview
To distinguish it from the `datetime` in python, numpy uses `datetime64 `.\
There are units , `Y, M, W, D, h, m, s, ms, NAT`. The min unit is `ms`.\
Normal parameter `dtype` construction, 
```python3
units = ['Y', 'M', 'W', 'D', 'h', 'm', 's', 'ms']
dtypes = [f"datetime[{unit}]" for unit in units]
```

# Generate
```python3
np.datetime64(dates, unit)
np.datetime64(dates, dtype)
```
`dates`:
1. time stamp
2. time delta, time from 1970

## Range
```python3
np.arange(time1, time2, dtype)
```

## Convert to string
```python3
np.datetime_as_string(time)
```

## Time delta
```python3
np.timedelta64(delta, unit)
```

## Weekday offset
```ptyhon3
np.busday_offset(date, offset, roll, weekmask, holiday)
```
`roll`, ['raise', 'nat', 'forward', 'following',
'backward', 'preceding', 
'modifiedfollowing', 'modifiedpreceding']
1. 'raise', raise error
2. 'nat', fill with `NaT`
3. 'forward' and 'following', the first valid day later in time.
4. 'backward' and 'preceding', the first valid day earlier in time.
5. 'modifiedfollowing', the first valid day later if in same month, else earlier in time.
6. 'modifiedpreceding', the first valid day earlier if in same month, else later in time.

Judge if is weekday
```python3
np.is_busday(time)
```

Count weekday
```python3
np.busday_count(start, end)
```