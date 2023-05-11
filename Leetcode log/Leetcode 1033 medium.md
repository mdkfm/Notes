# Link
[Leetcode 1033](https://leetcode.cn/problems/moving-stones-until-consecutive/)

# Mathematics Simulate
At first, we sort the list.
For min num, we have that We can complete the task in two steps.
For max num, We move the stones at both ends one unit by one unit until they are adjacent.
```python3
from typing import List


class Solution:
    def numMovesStones(self, a: int, b: int, c: int) -> List[int]:
        x, y, z = sorted([a, b, c])
        res = [2, z - x - 2]
        if ((z - y) == 1 and (y - x) == 1):
            res[0] = 0
        elif ((z - y) <= 2 or (y - x) <= 2):
            res[0] = 1
        return res
```