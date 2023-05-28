[toc]

## Link
[Leetcode 1079](https://leetcode.cn/problems/letter-tile-possibilities/)

## Answer
### Backtrack

```python3
from collections import Counter


class Solution:
    def numTilePossibilities(self, tiles: str) -> int:
        cnt = Counter(tiles)
        letter = set(tiles)

        def dfs(i):
            if i == 0:
                return 1
            res = 1 # end is a kind of situation
            for s in letter:
                if cnt[s] >= 1:
                    cnt[s] -= 1 # change
                    res += dfs(i - 1)
                    cnt[s] += 1 # restore
            return res
        
        # max len is len(tiles); minus res initialization
        return dfs(len(tiles)) - 1 
```

### Dp
We consider the num of permutations, 
using `j` letters and `i` kinds.

```python3
from collections import Counter
from math import comb

class Solution:
    def numTilePossibilities(self, tiles: str) -> int:
        counts = Counter(tiles).values()
        n, m = len(tiles), len(counts)
        
        # initialize dp 
        dp = [0] * (n + 1)
        dp[0] = 1
        
        # transitions
        for i, count in enumerate(counts, 1):
            tmp  = [0] * (n + 1)
            for j in range(n + 1):
                for k in range(min(j, count) + 1):
                    tmp[j] += dp[j - k] * comb(j, k)
            dp = tmp
        
        return sum(dp[1:]) 

```