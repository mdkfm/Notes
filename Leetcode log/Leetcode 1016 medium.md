# Link
[Leetcode 1016](https://leetcode.cn/problems/binary-string-with-substrings-representing-1-to-n/)

# Violent enumeration
Enumerate the binary of all nums.
```python3
class Solution:
    def queryString(self, s: str, n: int) -> bool:
        return all(bin(num)[2:] in s for num in range(1, n + 1))
```