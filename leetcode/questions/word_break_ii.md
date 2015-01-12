# Word Break
##### Problem
Given a string s and a dictionary of words dict, add spaces in s to construct a sentence where each word is a valid dictionary word.

Return all such possible sentences.

For example, given
```python
s = "catsanddog"
dict = ["cat", "cats", "and", "sand", "dog"]
```

A solution is `["cats and dog", "cat sand dog"]`.
##### Best Solution
```python
class Solution:
    # @param s, a string
    # @param dict, a set of string
    # @return a list of strings
    def wordBreak(self, s, dict):
        sentences = [[] for i in range(len(s))]
        wordLenList = set(map(len, dict))
        for startIndex in xrange(len(s) - 1, -1, -1):
            for wordLen in wordLenList:
                if startIndex + wordLen > len(s) or s[startIndex: startIndex + wordLen] not in dict:
                    continue
                if startIndex + wordLen == len(s):
                    sentences[startIndex].append(s[startIndex: startIndex + wordLen])
                else:
                    for sentence in sentences[startIndex + wordLen]:
                        sentences[startIndex].append(s[startIndex: startIndex + wordLen] + " " + sentence)
        return sentences[0]
```
##### Note
1. Bottom-up DP
    * Time Complexity: O(n)
    * Method
        * `sentences[i]` stores all sentences of `s[i:]`. `sentences[i] = [s[startIndex: startIndex + wordLen] + sentence for sentence in sentences[startIndex + wordLen] for wordLen in wordLenList]`
        * Update `sentences[i]` from end to the beginning of `s` 
        * A small optimization is at `for wordLen in wordLenList:`, where we only need to loop through all the possible word length.
        * Method: