# Longest Palindromic Substring

## Description

Given a string s, find the longest palindromic substring in s. You may assume that the maximum length of s is 1000.

## 思路

简单点说就是回文序列，难点应该就在回文的判断这一点了。在考虑这个问题的时候，我又想到了哈希表。主要是因为我并不希望在判断回文这一点上花费太多时间，从遍历的角度来看，整个字符串应该无论如何都是要过一遍的，所以时间复杂度应该要O(n)。基于字典，我可以通过下标来进行回文的判断。需要进行回文判断的情况主要是出现某个相同字符的时候，如果一个相同字符都没有的话，除非字符串本身就是单字符，否则不可能出现回文的情况。遇到相同字符的时候，需要更新一下回文字符串。最开始的回文可以设置为空，然后根据之前的字符串和当前字符串的长度可以进行判断。比较囧的是，我写了半天程序，总有用例过不去，感觉这个思路不太好。最后我参考了一下其他人的博客，实际上我的思路应该很接近了，但是因为我总盯着O(n)不放，所以写出来的代码总是有问题。如果把限制从O(n)调整到O(n^2)，其实还是有办法的。首先需要遍历整个字符串，然后在遍历的时候，每扫过一个字符，就以该字符为中心像两边扫描直到没有回文为止。另外一种方案是Manacher算法。

## 代码

```

class Solution(object):
    def longestPalindrome(self, s):
        """
        :type s: str
        :rtype: str
        """
        len_s = len(s)
        longest_p = '' # The longest palindrome
        if (len_s == 0):
            return ''
        for i in range(len_s * 2 - 1):
            left = right = i // 2
            if i % 2 == 1:
                right += 1
            sample = self.palindrome(s, left, right)
            if len(longest_p) < len(sample):
                longest_p = sample
        return longest_p
            
        
    def palindrome(self, s, left, right):
        while left >= 0 and right < len(s) and s[left] == s[right]:
            left -= 1
            right += 1
        return s[left+1 : right]
```

## 总结

字符串确实是自己的弱项，不过也是没想到会这么弱。看了别人的代码之后真是恍然大悟，我在看了思路的情况下直接写其实遇到了不少问题。因为回文的字符串可以分为奇数和偶数两种情况，我自己写的时候又只遍历一遍字符串，使得我很难兼顾两种不同的字符串。但是别人直接用len*2这种手段，然后通过除法就可以做到每个字符访问两次，然后再根据这两次来进行不同类型回文字符串的判断。Manacher就等到我第二次刷的时候再来考虑了。