# Minimum Window Substring

## Description

Given a string S and a string T, find the minimum window in S which will contain all the characters in T in complexity O(n).

## 思路

这个题一开始我以为和字符串匹配是差不多的，但是实际想过之后觉得不对。因为这里中间是可以包含其他字符来的，难度上应该是又增加了。按照题目给的案例，甚至连匹配串的字符顺序都不用管，从思路上来讲又麻烦了很多。我能想到的方法就是之前用过的字典，因为字典可以存储已经访问过的字符的index，根据这个index我们可以再做判断。但是问题在于，遇到重复字符的时候不好处理。最后还是看了一下其他人的解法，基本上也是使用了哈希表。但是这里面并没有存储index，而是在匹配串T中各个字符出现的次数。也就是当次数变为0的时候，该字符就已经满足条件了。最开始需要遍历T，将对应字符出现次数存到哈希表中。然后开始遍历S，遇到T中的字符，就把哈希表中的value减1，直到包含了所有T中字符为止。当找到了对应字符串的时候，如果该字符串是比较短的那个，那就存下来。实际上遍历中间也有一点问题，因为当开始遍历之后，是从某一个字符串开始的。一旦找到了一个满足条件的子串，那么应当从这个字符的下一个字符开始找起。

## 代码

``` python
class Solution:
    def minWindow(self, s, t):
        """
        :type s: str
        :type t: str
        :rtype: str
        """
        if len(t) > len(s):
            return ''
        dic = {}
        res = ''
        for c in t:
            if c in dic:
                dic[c] += 1
            else:
                dic[c] = 1
        left, right, count, minLen = 0, 0, 0, len(s) + 1
        while right < len(s):
            if s[right] in dic and right < len(s):
                dic[s[right]] -= 1
                if dic[s[right]] >= 0:
                    count += 1
                while count == len(t):
                    if right - left + 1 < minLen:
                        minLen = right - left + 1
                        res = s[left:right+1]
                    if s[left] in dic and left < len(s):
                        dic[s[left]] += 1
                        if dic[s[left]] > 0:
                            count -= 1
                    left += 1
            right += 1
        return res
```

## 总结

这道题的思路属于比较巧妙的类型，因为当访问到了第一个符合条件的子串的时候，left起到了一个很大的作用。利用left我们可以直接从当前的子串里去除掉一个属于t中字符，然后接着寻找到下一个字符。这样每次寻找并不是单纯的从头开始找，而是根据已经找到的一个子串来继续寻找。