# Statistics
[numpy statistics](https://numpy.org/doc/stable/reference/routines.statistics.html)

Usual parameters `axis, keepdim`.\
```python3
np.amax(arr)
np.amin(arr)
np.sum(arr)
np.cumsum(arr)
```

## Mean and deviation
```python3
np.average(arr)

np.mean(arr)
np.nanmean(arr)

np.std(arr)
np.nanstd(arr)

np.var(arr)
np.nanvar(arr)
```

## Quantile
```python3
np.median(arr)
np.nanmedian(arr)

np.quantile(arr, q)
np.nanquantile(arr, q)

np.percentile(arr, q)
np.nanpercentile(arr, q)
```

## `ptp`
```python3
np.ptp(arr)
```
Range of values (maximum - minimum) along an axis.

# Correlate
```python3
np.correlate(a, b, mode)
```
`mode`, {'valid', 'same', 'full'}, default valid.

```python3
np.corrcoef(a, v, rowvar)
```
`rowvar`, bool, whether is row variable or not.
$$
R_{ij} = \frac{ C_{ij} } { \sqrt{ C_{ii} * C_{jj} } }
$$

```python3
np.cov(m, y, rowvar, bias, ddof, fweights, aweights)
np.cov(m, rowvar, bias, ddof, fweights, aweights)
```
$$
\operatorname{cov}_{x, y}=\frac{\sum\left(x_{i}-\bar{x}\right)\left(y_{i}-\bar{y}\right)}{N-1}
$$

# Histogram
## One dimension
```python3
np.histogram(a, bins, range, density, weights)
```
`bins`, list or int.
`density`, bool, default `False`.

## Two dimensions
```python3
had, xe, ye = np.histogram2d(x, y, bins, range, density, weights)
```
`x`, `y`, arrays with one dimension.\
`bins`:
- shared: int, array
- separately: [int, int], [array, array]
- int denotes the num of bins, array includes the bounds.

`had`, array, histogram.
`xe`, `ye`, arrays that include the bounds.

## Multi-dimension
```python3
had, edges = np.histogramdd(arr, bins, range, density, weights)
```
`arr`, array with two dimension.\
Every column is regarded as a variable.\
`edges`, list of arrays that include the bounds.

## Calculate bounds
```python3
histogram_bin_edges(a, bins, range, weights)
```
`bins`, int, array, str.
When `bins` is str, 
{'auto', 'fd', 'doane', 'scott', 'stone', 'rice', 'sturges', 'sqrt'}.

## Digitize
```python3
np.digitize(x, bins)
```
Digitize `x`, use the indices of interval defined by `bins`.

# Count
```python3
out = np.bin_count(a, weigths, minlength)
```
`a`, array_like, 1 dimension, nonnegative ints.\
`weights`, array_like with same shape as `a`.\
`minlength`, int, the min length of `out`.\
`out`, array_like, 1 dimension.

```python3
np.count_nonzero(a)
```

# Random generator
Numpy uses `BitGenerator` to generate a random sequence, 
then uses `Generator` to transfer it to given distribute.

`BitGenerator`:
- PCG64
- PCG64DXSM
- MT19937
- Philox
- SFC64

Create a `BitGenerator`
```python3
bg = np.random.PCG64(seed=42)

# Use the entropy of system as seed
ss = np.random.SeedSequence()
bgr = np.random.PCG64(ss.entropy)
```

Use `Generator`
```python3
rng = np.random.Generator(bg)

rng.stand_normal()

rng.bit_generator is bg # True
```

## Parallel
### Method 1, `SeedSequence spawning`
Use `SeedSequence spawning` to generate child seeds.
```python3
import multiprocessing

threads_num = multiprocessing.cpu_count()

ss = np.random.SeedSequence(seed=42)
child_seeds = ss.spawning(threads_num) 
bgs = [np.random.PCG64(s) for s in child_seeds]
streams = [np.random.Generator(bg) for bg in bgs]
```

### Method 2, `Philox`
`Philox` uses weak cryptographic primitives 
to encrypt up counters to generate values.
```python3
import secrets
import multiprocessing

threads_num = multiprocessing.cpu_count()
root_seed = secrets.randbits(128) # 128 bits, weak cryptographic primitive 

bgs = [
    np.random.Philox(key=root_seed + stream_id)
    for stream_id in range(threads_num)
]
```

### Method 3, `jump`
Use `jump` to greatly advance the status of `BitGenerator`.

| BitGenerator| 周期        | jump大小  | 位数/每次抽取|
|:------------|:----------|:--------|:-------|
| PCG64       | 2^128     | 2^127   | 64     |
| PCG64DXSM   | 2^128     | 2^127   | 64     |
| MT19937     | 2^19937-1 | 2^128   | 32     |
| Philox      | 2^256     | 2^128   | 64     |

```python3
bg = np.random.PCG64(seed)
bgs = [bg.jumped(i) for i in range(num)]
```
We could see the `state` of `bg`
```python3
bg.state
```

### Note
The use of `PCG64` in Massively parallel environments 
has proved to have statistical weaknesses.\
NumPy has introduced a new `PCG64DXSM`, 
which will eventually become the engine of `default_rng` in future versions of RNG.


## Multiprocessing
Example,
```python3
from numpy.random import default_rng, SeedSequence
import multiprocessing
import concurrent.futures
import numpy as np

class MultithreadedRNG:
    def __init__(self, n, seed=None, threads_num=None):
        if threads_num is None:
            threads_num = multiprocessing.cpu_count()
        
        self.threads_num = threads_num

        seq = SeedSequence(seed)
        
        # use spawn to get Generators of `threads_num`
        self._random_generators = [default_rng(s)
                                   for s in seq.spawn(threads_num)]

        self.n = n
        # get the corresponding executor
        self.executor = concurrent.futures.ThreadPoolExecutor(threads_num)
        # store values
        self.values = np.zeros(n)

        self.step = np.ceil(n / threads_num).astype(np.int_)

    def fill(self):
        # fill random values
        # random, standard_normal, standard_exponential, standard_gamma支持
        def _fill(random_state, out, first, last):
            # fill into `out`
            random_state.standard_normal(out=out[first:last])

        futures = {}
        for i in range(self.threads_num):
            # multiprocess
            args = (_fill,
                    self._random_generators[i],
                    self.values,
                    i * self.step,
                    (i + 1) * self.step)
            futures[self.executor.submit(*args)] = i
        concurrent.futures.wait(futures)

    def __del__(self):
        self.executor.shutdown(False)
```
This could improve performance and save time.\
Test
```python3
N = 10000000
seed = 42
mrng = MultithreadedRNG(N, seed=seed)
mrng.fill() # 11.8ms

values = np.zeros(N)
rg = np.random.default_rng()
%timeit rg.standard_normal(out=values) # 88.1ms
```

## Generator performance
Refer to [Generator performance](https://numpy.org/devdocs/reference/random/performance.html)


# Choice and shuffle
## Choice
```python3
rng = np.random.default_rng(seed)
rng.choice(a, size, replace, p)
```
`a`, {array_like, int},
corresponding choice from `a` or `np.arange(a)`.\
`replace`, bool, whether put elements back.\
`p`, probability list.

## Shuffle
In place.
```python3
rng.shuffle(a, axis)
```

Not in place.
```python3
rng.permutation(a, axis)
```

Shuffle independently.
```python3
rng.premuted(a, axis, out)
```

# Random distributes
At first, we choose a generator.
```python3
rng = np.random.default_rng(42)
```

## Int
```python3
rng.integers(low, high, size, dtype, endpoint)
```
`endpoint`, bool, whether concludes `high` or not.

## Decimal
```python3
rng.random(size) 
rng.uniform(low, high, size)
```

## Normal
```python3
rng.standard_normal(size, dtype, out)
rng.normal(loc, scale, size)
rng.multivariate_normal(locs, cov, size)
```
More refer to [RNG](https://numpy.org/doc/stable/reference/random/generator.html)

Follow distributes have familiar shape. 
```python3
rng.lognormal()
rng.laplace()
rng.rayleigh()
rng.gumbel()
rng.standard_cauchy()
rng.vonmises()
rng.wald()
rng.triangular(left, mode, right)
```

## Dispersed
### Binomial
```python3
rng.binomial(n ,p, size)
rng.multinomial(n, p, size)
```
`n`, the num of experiments.\
`p`, probability.\
Return the times of success.

### Negative binomial
```python3
rng.negative_binomial(n, p, size)
```
`n`, the times of success.\
Return the times of failure.


### Possion
```python3
rng.possion(lam, size)
```
$$
f(k; \lambda)=\frac{\lambda^k e^{-\lambda}}{k!}
$$


### Geometric
```python3
rng.geometric(p, size)
```
$$
f(k) = (1 - p)^{k - 1} p
$$


### Hyper geometric
```python3
rng.hypergeometric(ngood, nbad, nsample, size)
```
$$
P(x) = \frac{\binom{g}{x}\binom{b}{n-x}}{\binom{N}{n}}\\
g=\text{good}, b=\text{bad}
$$


Multivariate hyper-geometric

$$
f(x)=\frac{\left(\begin{array}{c}
D \\
x
\end{array}\right)\left(\begin{array}{c}
N-D \\
n-x
\end{array}\right)}{\left(\begin{array}{c}
N \\
n
\end{array}\right)}
$$

```python3
rng.multivariate_hypergeometric(colors, nsample, size, method)
```
`color`, list of int, 
the number of each type of item 
in the collection from which a sample is drawn.\
`method`, {'marginals', 'count'}.

We could simulate two methods easily.
```python3
# count
choices = np.repeat(np.arange(len(colors)), colors)
selection = rng.choice(choices, nsample, replace=False)
variate = np.bincount(selection, minlength=len(colors))
```
```python3
# Marginals
variate = np.zeros(len(colors), dtype=np.int64)
remaining = np.cumsum(colors[::-1])[::-1]
for i in range(len(colors) - 1):
    if nsample < 1:
        break
    variate[i] = rng.hypergeometric(colors[i], remaining[i+1], nsample)
    nsample -= variate[i]
variate[-1] = nsample
```

## Exponent and logarithm

### Power
```python3
rng.power(a, size)
```
$$
P(x; a) = ax^{a-1}, 0 \le x \le 1, a>0
$$

### Pareto
```python3
rng.pareto(a, size)
```

$$
p(x) = \frac{am^a}{x^{a+1}}
$$

### Zeta
```python3
rng.zipf(a, size)
```

$$
p(k) = \frac{k^{-a}}{\zeta(a)}
$$

### Beta
```python3
rng.beta(a, size)
```

$$
f(x; a,b) = \frac{1}{B(\alpha, \beta)} x^{\alpha - 1}
(1 - x)^{\beta - 1},\\
B(\alpha, \beta) = \int_0^1 t^{\alpha - 1}
(1 - t)^{\beta - 1} dt.
$$

### Dirichlet
```python3
rng.dirichlet(alpha, size)
```
`alpha`, sequence of floats, length k.\
Output: The drawn samples, of shape (size, k).

$$
{\displaystyle f(x_{1},\dots ,x_{K};\alpha _{1},\dots ,\alpha _{K})={\frac {1}{\mathrm {B} (\alpha )}}\prod _{i=1}^{K}x_{i}^{\alpha _{i}-1}}
$$

### Gamma
```python3
rng.gamma(shape, scale, size)
```
`shape`, the `k` value of gamma distribution.\
`scale`, the `theta` value of gamma distribution.

$$
p(x) = x^{k-1}\frac{e^{-x/\theta}}{\theta^k\Gamma(k)}
$$

### Exponential
```python3
rng.exponential(scale, size)
```
`scale`, the `1 / beta`.\
$$
f(x; \frac{1}{\beta}) = \frac{1}{\beta} \exp(-\frac{x}{\beta})
$$

### Weibull
```python3
rng.weibull(a, size)
```
$$
p(x) = \frac{a}{\lambda}(\frac{x}{\lambda})^{a-1}e^{-(x/\lambda)^a}
$$


### Log series
```python3
rng.logseries(p, size)
```
$$
P(k) = \frac{-p^k}{k \ln(1-p)}
$$

### Logistic
```python3
rng.logistic(loc, scale, size)
```
$$
P(x) = \frac{e^{-(x-\mu)/s}}{s(1+e^{-(x-\mu)/s})^2}
$$

## For checking
### Chisquare
```python3
rng.chisquare(df, size)
```
$$
p(x) = \frac{(1/2)^{k/2}}{\Gamma(k/2)}
x^{k/2 - 1} e^{-x/2}
$$

```python3
rng.noncentral_chisquare(df, nonc, size)
```
$$
P(x;df,nonc) = \sum^{\infty}_{i=0} \frac{e^{-nonc/2}(nonc/2)^{i}}{i!} P_{Y_{df+2i}}(x)
$$

### F
```python3
rng.f(dfnum, dfden, size)
rng.noncentral_f(dfnum, dfden, nonc, size)
```

### T
```python3
rng.stasndard_t(df, size)
```
