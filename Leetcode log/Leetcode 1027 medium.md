[toc]

# Link
[Leetcode 1027](https://leetcode.cn/problems/longest-arithmetic-subsequence/)

# Analysis
Obviously, we could get the answer in one traverse.
We use a dp dict, dp[(num, d)] is the max length of arithmetic subsequence with public errand "d" and last num "num"  during traversing.
```python3
class Solution:
    def longestArithSeqLength(self, nums: List[int]) -> int:
        seen = set() # visited num
        dp = dict()

        for num in nums:
            for last in seen:
                d = num - last
                dp[(num, d)] = dp.get((last, d), 1) + 1 
            seen.add(num)
        
        return max(dp.values())
```
