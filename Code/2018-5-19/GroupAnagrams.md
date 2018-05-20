# Group Anagrams

## Description

Given an array of strings, group anagrams together.

## 思路

这道题需要解决的问题就在于，如果两个单词构成的字母相同，那就把他们归类在一起。感觉和之前做的那个求有多少Permutation的类似，但是思路其实反过来了。现在要做的就是每次找result中的每一项，然后比对字母，如果相同就加入，不相同就加入一个新的数组中。最开始的时候我是用set来解这个题目，但是后面提交发现还是会有问题，比如bob和boo这两个会算作不同的字符串。对于这种情况，我主要思路就是利用counter来解决问题了，但是问题是我要如何取统计这些字符的出现。参考了一下其他人的解法， 其实主要是利用sorted方法和字典，sort之后的字符串基本上就可以判断了，然后sort之后的值作为key值来加入就可以了。

## 代码

``` python
class Solution:
    def groupAnagrams(self, strs):
        """
        :type strs: List[str]
        :rtype: List[List[str]]
        """
        grouped = {}
        for s in strs:
            grouped.setdefault(''.join(sorted(s)), []).append(s)

        return list(grouped.values())
```

## 总结

这个题目非常容易想到set，但是set其实行不通，因为有字符串出现次数的问题。继而容易想到利用count来计算，但是会是问题更复杂。其实直接利用sort和字典就可以比较轻松地解决问题。