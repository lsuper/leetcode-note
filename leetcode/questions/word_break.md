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
        self.isBreakable = [False] * len(s)
        self.dict = dict
        lenLst = [len(entry) for entry in dict]
        self.maxLen = max(lenLst)
        self.minLen = min(lenLst)
        self.updateWordBreak(s)
        return self.isBreakable[0]
        
    def updateWordBreak(self, s):
        self.isBreakable[-1] = s[-1] in self.dict
        if len(s) == 1:
            return
        #from end to beginning
        for index in range(len(s)-2, -1, -1):
            #optimize point, here we can (a) check all words in dict or (b) check all valid length in s[index: index+wordLen]
            #if len(dict) < maxLen - minLen, use (a), otherwise use (b)
            for wordLen in range(self.minLen, self.maxLen+1):
                if index + wordLen - 1 <= len(s) - 1:
                    if s[index:index+wordLen] in self.dict and (index+wordLen == len(s) or self.isBreakable[index + wordLen]):
                        self.isBreakable[index] = True
                        continue
        return
        
```
##### Note
1. Method 1
    * Time Complexity:
        * Method:

--------------

