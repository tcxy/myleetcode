# Longest Substring Without Repeating Charaters

## Description

Given a string, find the length of the longest substring without repeating characters.

## 思路

核心思路应该是遍历字符串然后根据字符来判断是否重复。字符串需要遍历一边，复杂度应该至少是O(n)。对于已经访问的字符串也需要进行遍历，最坏的情况是可以到O(N^2)。这道题让我想到了第一题，在那道题里面利用了哈希表的特性来实现以访问过数据的快速查找，这里也可以利用相似的技巧。故而可以用字典来存储已经访问过的数据，问题在于键值对应该选择什么。一开始我觉得可以用字符做键，然后用0和1来标识访问过没有。但是考虑了一下这样是不行的，因为一旦出现重复字符，要把所有已访问的字符清空。重新考虑之后我觉得可以用字符为键，下标为值，这样的话，每次直接寻找是否存在相应字符，不存在的话就存入当前下标。存在的话，由已存的下标和当前的下标来判断是否重复。这样的话，我还需要一个变量来表示当前的子串的起始点。

## 代码

```

class Solution(object):
    def lengthOfLongestSubstring(self, s):
        """
        :type s: str
        :rtype: int
        """
        s_length = len(s) # length of s
        if s_length == 1:
            return 1
        sub_index = 0 # The start index of substring
        accessed_char = {} # The character that we've accessed
        longest = 0 # Longest length of substring
        for index, value in enumerate(s):
            if value in accessed_char and sub_index <= accessed_char[value]:
                # Duplicate char 
                longest = max(longest, index - sub_index)
                sub_index = accessed_char[value] + 1                
            accessed_char[value] = index
        if s_length - sub_index > longest and s[s_length - 1] != s[sub_index]:
            longest = s_length - sub_index
        return longest
                
```

## 总结

整体来说这段代码写得非常纠结，一开始我直接返回了substring。然后发现要返回最长的长度，于是我采用了现在的这些变量。但是写起来还是非常麻烦的，因为总会缺少部分判断，比如我一开始的长度判断，如果我不判断最后一个字符的话那就不需要最开始的这个判断。但是不判断最后一个字符是否重复的话会遇到刚好在最后一个字符重复的情况，而且for内部的判断容易写出问题，总的来说思路还没有彻底理顺。参考答案之后发现基本都是这个思路，不过有人直接在for里面更新longest的值了，这样就可以丢到两层判断，但是每次循环都要多做一个比较，两种方案不好说谁好谁坏，但是美观性上来说还是人家好一点。