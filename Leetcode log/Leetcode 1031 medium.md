# Link
[Leetcode 1031](https://leetcode.cn/problems/maximum-sum-of-two-non-overlapping-subarrays/)

# From tarverse to dp

## Traverse
At first, we want to calculate the sum of the elements of subarray.
Prefix list could make it.
We consider two situations that firstLen before secondLen or secondLen before firstLen
```python3
class Solution:
    def maxSumTwoNoOverlap(self, nums: List[int], firstLen: int, secondLen: int) -> int:
        prefix = [0]
        cur = 0
        for num in nums:
            cur += num
            prefix.append(cur)

        n = len(nums)

        def max_sum(firstLen, secondLen):
            res = 0
            for i in range(firstLen, n + 1):
                first_sum = prefix[i] - prefix[i - firstLen]
                for j in range(i + secondLen, n + 1):
                    second_sum = prefix[j] - prefix[j - secondLen]
                    res = max(res, first_sum + second_sum)
            return res

        return max(max_sum(firstLen, secondLen), max_sum(secondLen, firstLen))

```
This answer use twice two nested traverses to find the best match and use prefix list to simple the calculation of sum.
The complexity of time is $\Theta(n^2)$. The complexity of cache is $\Theta(n)$

## Dp
If we fix the second window, then calculate the max first window. We could find that the calculation of the first could be simplified by dp.
```python3
class Solution:
    def maxSumTwoNoOverlap(self, nums: List[int], firstLen: int, secondLen: int) -> int:
        return max(self.calculate(nums, firstLen, secondLen), self.calculate(nums, secondLen, firstLen))

    def calculate(self, nums, firstLen, secondLen):
        suml = 0
        for i in range(0, firstLen):
            suml += nums[i]
        maxSumL = suml  # dp list of one element
        sumr = 0  # sum of fixed win
        for i in range(firstLen, firstLen + secondLen):
            sumr += nums[i]
        res = maxSumL + sumr
        j = firstLen
        for i in range(firstLen + secondLen, len(nums)):
            suml += nums[j] - nums[j - firstLen]
            maxSumL = max(maxSumL, suml)  # update dp
            sumr += nums[i] - nums[i - secondLen]  # slip the second win
            res = max(res, maxSumL + sumr)
            j += 1
        return res
```