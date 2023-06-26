[toc]

# Link
[Leetcode 2559](https://leetcode.cn/problems/count-vowel-strings-in-ranges/)

# Prefix Sum
We could use prefix sum array to construct any query.
```python3
class Solution:
    def vowelStrings(self, words: list[str], queries: list[list[int]]) -> list[int]:
        # construct prefix
        vowel = set("aeiou")
        prefix = [0]
        for word in words:
            prefix.append(prefix[-1])
            if word[0] in vowel and word[-1] in vowel:
                prefix[-1] += 1
                
        # construct res according to prefix
        res = []
        for l, r in queries:
            res.append(prefix[r + 1] - prefix[l])
        return res
```