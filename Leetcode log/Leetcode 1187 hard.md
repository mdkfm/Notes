[toc]

# Link
[Leetcode 1187](https://leetcode.cn/problems/make-array-strictly-increasing/)
# A Wrong Trial
```python3
class Solution:
    def makeArrayIncreasing(self, arr1: List[int], arr2: List[int]) -> int:
        arr2.sort()
        n = len(arr1)
        m = len(arr2)
        def calulate(i: int, j: int, bottom: int) -> int:
            print(i, j, bottom)
            if i == n:
                return 0
            while j < m and arr2[j] <= bottom:
                j += 1   
            if j >= m:
                while i < n and arr1[i] > bottom:
                    bottom = arr1[i]
                    i += 1
                if i == n:
                    return 0
                return None

            res = n
            if (num1 := calulate(i + 1, j, arr1[i])) is not None and arr1[i] > bottom:
                res = min(res, num1)
            if (num2 := calulate(i + 1, j, arr2[j])) is not None:
                res = min(res, num2 + 1)
            if num1 is None and num2 is None:
                return None
            return res
        
        if (res := calulate(0, 0, -1)) is not None:
            return res
        else:
            return -1
```

I try to use a recursion function to solve this question.But WA.
Use two index i and j to quote elements from arr1 and arr2.
For process calculate(i, j, bottom), parameter bottom is the last element arr1[i - 1], and I consider two situations, changing arr[i] or not.


# Answer and Correction

## DP answer
```python3
from bisect import bisect_right
from typing import List


class Solution:
    def __init__(self):
        self.inf = float("inf")

    def makeArrayIncreasing(self, arr1: List[int], arr2: List[int]) -> int:
        arr2 = sorted(set(arr2))
        n = len(arr1)
        m = len(arr2)
        dp = [[self.inf] * (min(m, n) + 1) for _ in range(n + 1)]
        dp[0][0] = -1
        for i in range(1, n + 1):
            for j in range(min(i, m) + 1):
                if arr1[i - 1] > dp[i - 1][j]:  # situation 1
                    dp[i][j] = arr1[i - 1]
                if j and dp[i - 1][j - 1] != self.inf:  # situation 2
                    k = bisect_right(arr2, dp[i - 1][j - 1], j - 1)
                    if k < m:
                        dp[i][j] = min(dp[i][j], arr2[k])
                if i == n and dp[i][j] != self.inf:
                    return j
        return -1
```

In this answer, we use a dp list, dp[i][j] is the min value of the last element arr[i] with j times changing. Initialize dp[0][0] with -1, others with inf.
For every state, dp[i][j] could  transite from dp[i - 1][j - 1] or dp[i - 1][j], one situation reserves arr1[i] and other not.

## DP Optimize
This above dp function could be optimized. Consider a new dp function, dp[i] is the min times of changing that reserves arr1[i].
```python3
from bisect import bisect_left
from typing import List 


class Solution:
    def __init__(self):
        self.inf = float("inf")

    def makeArrayIncreasing(self, arr1: List[int], arr2: List[int]) -> int:
        arr1 = [-1] + arr1 + [self.inf]
        arr2 = sorted(set(arr2))
        n = len(arr1)
        m = len(arr2)
        dp = [self.inf for i in range(n)]
        dp[0] = 0
        for i in range(1, n):
            if arr1[i] > arr1[i - 1]:  # situation 1
                dp[i] = dp[i - 1]

            ind = bisect_left(arr2, arr1[i]) - 1 # find max in arr2 < arr1[i]
            for j in range(1, min(i - 1, ind) + 1): # situation 2
                if arr1[i - j - 1] < arr2[ind - j + 1]:
                    dp[i] = min(dp[i], dp[i - j - 1] + j)
        return dp[n - 1] if dp[n - 1] != self.inf else - 1
```
We add two sentinel into arr1, -1 at head and inf at tail. These two would not be changed according their value.
Situation first, arr1[i] > arr1[i - 1], the dp[i] could be transtie from dp[i - 1].
Situation second, the dp[i] could be transtie from dp[i - j -1] where 1 <= j <= min(i - 1, ind), with j elements from arr1[i - j] to arr1[i - 1] changed, dp[i] = min(dp[i], dp[i - j - 1] + j). 