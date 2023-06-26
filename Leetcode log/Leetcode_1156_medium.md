# Link
[Leetcode](https://leetcode.cn/problems/swap-for-longest-repeated-character-substring/)

# Rolling
We could use a rolling window to find the longest repeated substring. 
```python3
class Solution:
    def maxRepOpt1(self, text: str) -> int:
        count = Counter(text)
        res = 0
        for i in range(len(text)):
            j = i
            while j < len(text) and text[j] == text[i]:
                j += 1
            
            # Find another longest substring separated by a character 
            k = j + 1
            while k < len(text) and text[k] == text[i]:
                k += 1
            res = max(res, min(k - i, count[text[i]]))
            i = k - 1
        return res
```