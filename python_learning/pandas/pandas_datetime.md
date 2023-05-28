[toc]

# Overview

| Definition   | Element type | Series type      | Pandas data type  |
|:-------------|:-------------|:-----------------|:------------------|
| Date times   | `Timestamp`  | `DatetimeIndex`  | `datetime64[ns]`  |
| Time deltas  | `Timedelta`  | `TimedeltaIndex` | `timedelta64[ns]` |
| Time spans   | `Period`     | `PeriodIndex`    | `period[freq]`    |
| Date offsets | `DateOffset` | `None`           | `None`            |

# Date times

## Timestamp
```python3
pd.Timestamp(year, month, day, hour, minute, second)
pd.Timestamp(ts_input)
```
Keyword arguments `year, month, day, hour, minute, second`, 
used to determine a timestamp.\
`ts_input` is a time str.

### Instance attributes
Attributes `year, month, day, hour, minute, second`, 
get the time.\
`value`, the num of nanoseconds 
from zero on January 1, 1970(Computer Year) 
to the given timestamp.

### Class attributes
`max, min`, the max and min timestamp.

## Datetime series

### `to_datetime`
```python3
pd.to_datetime(arg, formatstr, )
```
`arg`, int, float, str, datetime, list, tuple, 1-d array, Series, DataFrame/dict-like\
The object to convert to a datetime.\
If a DataFrame is provided, the method expects minimally the following columns: "year", "month", "day".

`errors`, {'ignore', 'raise', 'coerce'}, default 'raise'.\
For a invalid parsing,
+ 'raise', raise an exception.
+ 'coerce', set as NaT.
+ 'ignore', return the input.

`formatstr`, default None. The `strftime` to parse time.\
Refer to [strftime documentation](https://docs.python.org/3/library/datetime.html#strftime-and-strptime-behavior).

### Range

```python3
pd.date_range(start=None, end=None, 
              periods=None, freq=None,
              tz=None, normalize=False,
              name=None, inclusive='both',
              *, 
              unit=None, **kwargs)
```
`freq` is the frequence, auto specified as 'D'.\
`tz` is time zone.\
`normalize`, bool, default `False`,
whether normalize start/end dates to midnight.\
`inclusive`, {'both', 'neither', 'left', 'right'}, default 'both',
whether to set each bound as closed or open.

`bdate_range`, used to gen a series without holidays.
```python3
pd.bdate_range(start=None, end=None,
               periods=None, freq='B',
               tz=None, normalize=True,
               name=None,
               weekmask=None, holidays=None,
               inclusive='both',
               **kwargs)
```
`freq`, must specified.\
`weekmask`, str, 
mask of valid business days, 
passed to `numpy.busdaycalendar`
auto specified as 'Mon Tue Wed Thu Fri'.\
`holidays`, list-like,
dates to exclude from the set of valid business days,
passed to `numpy.busdaycalendar`.

### Change `freq`
```python3
s.asfreq(freq, 
         method=None, how=None,
         normalize=False,
         fill_value=None)
```
`method`, {'backfill'/'bfill', 'pad'/'ffill'}, default `None`\
`how`, {'start', 'end'}, default end, for `PeriodIndex` only.
`fill_value`, scalar,
value to use for missing values, applied during upsampling.

## `dt` object
```python3
s.dt
```
Normal attributes, 
`date, 
time, year, month, day, hour, minute, second, microsecond, nanosecond,
dayofweek, dayofyear, weekofyear, daysinmonth,
quarter`

Returning a bool value, 
```python3
s.dt.is_year_start
s.dt.is_quarter_start
s.dt.month_start

s.dt.is_year_end
s.dt.is_quarter_end
s.dt.is_month_end
```

Round, 
```python3
s.dt.round(freq)
s.dt.ceil(freq)
s.dt.floor(freq)
```

# Timedelta

## Generate
Generate a `pd.Timedelta`,
```python3
pd.Timedelta(days, months, ...)
pd.Timedelta(time_str)

timestamp1 - timestamp2 # return a pd.Timedelta
```
Generate a `pd.Series`,

```python3
pd.to_timedelta(s)
pd.timedelta_range(start, end, freq, period)
```

## Calculation
```python3
timestamp1 - timestamp2 # return a pd.Timedelta
timestamp + timedelta # return a pd.Timestamp
```

# Offset

## Offset methods
We could  check all offset methods, using  
```python3
pd.offsets.__all__
```

There are some usual offset methods.
```python3
pd.offsets.Day()
pd.offsets.BDay()
pd.offsets.CDay()
pd.offsets.WeekofMonth()
pd.offsets.MonthBegin()
pd.offsets.MonthEnd()
```

## Offset strings
We could use offset strings to denote offsets as parameter `freq`.

| String       | Offset                         |
|:-------------|:-------------------------------|
| 'MS'         | MonthBegin()                   |
| 'M"          | MonthEnd()                     |
| 'B'          | BDay()                         |
| 'W-MON'      | CDay(weekmask='Mon')           |
| 'WOM-1MON'   | WeekOfMonth(week=0,weekday=0)  |

More refer to [Offset aliases](https://pandas.pydata.org/docs/user_guide/timeseries.html#offset-aliases).


# Date rolling and resample

## Rolling
When the data type of index is `datetime64[ns]`, we could use date rolling.
```python3
s.rolling(time)
```
It has same attributes and methods with normal rolling.

## Shift
A slide method of series with time index.
```python3
s.shift(freq)
```

## Resample
It is same with `groupby`, specified to datetime series.
```python3
s.resample(rule, origin)
```
`rule`, DateOffset, Timedelta or str,
the offset string or object representing target conversion.\
`origin`, {'epoch', 'start', 'start_day'}, 
Timestamp or str, default 'start_day'.
- 'epoch': 1970-01-01
- 'start': the first value of the timeseries
- 'start_day': the first day at midnight of the timeseries