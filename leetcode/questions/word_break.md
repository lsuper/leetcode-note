# Word Break
##### Problem
Given a string `s` and a dictionary of words `dict`, determine if `s` can be segmented into a space-separated sequence of one or more dictionary words.

For example, given
```python
s = "leetcode",
dict = ["leet", "code"].
```

Return `true` because `"leetcode"` can be segmented as `"leet code"`.
##### Best Solution
```python
class Solution:
    # @param s, a string
    # @param dict, a set of string
    # @return a boolean
    def wordBreak(self, s, dict):
        if len(dict) < 1:
            return False
        isBreakable = [False] * len(s)
        lenLst = set(map(len, dict))
        #from end to beginning
        for index in range(len(s)-1, -1, -1):
            #optimize point, here we can (a) check all words in dict or (b) check all valid length in s[index: index+wordLen]
            #if len(dict) < maxLen - minLen, use (a), otherwise use (b)
            for wordLen in lenLst:
                if index + wordLen <= len(s):
                    if s[index:index+wordLen] in dict and (index+wordLen == len(s) or isBreakable[index + wordLen]):
                        isBreakable[index] = True
                        continue
        return isBreakable[0]
```
##### Note
1. Bottom-up DP
    * Time Complexity: $$O(n)$$
    * Method
        * `isBreakable[i]` represents whether `s[i:]` can be separated into  a sentence. `isBreakable[i] = s[index:index+wordLen] in dict and (isBreakable[index + wordLen] or s[index:index+wordLen] is last word in sentence)`. No need to initialize the state function. 

--------------

