# Regular Expression Matching 

## Project description

Given an input string (s) and a pattern (p), implement regular expression matching with support for '.' and '*'.

```
'.' Matches any single character.
'*' Matches zero or more of the preceding element.
```

The matching should cover the entire input string (not partial).

## 思路

这题直接failed了，感觉思考的方向完全不对。我一开始打算直接访问s上的每一个字符，然后由这个字符作为起点来进行对比。但是对比的过程比较难把握，尤其是\*这个符号的使用，不含\*的情况需要两个字符串长度一致，而包含了\*就麻烦了，一来需要判断\*之前是什么字符。二来需要根据\*之后的字符进行判断，但是当p遍历完了之后也不见得就是一个符合的字符串，还是要根据长度来进行判断。我觉得最难的情况就像是"aaa"和“a*a"这样的字符串进行比对，因为不好界定\*号到底指代什么，如果按最大长度来指代那这个表达式反而不匹配了。如果按最小的话倒是可行，但是照这种思路，需要判断的条件太多了，和\*相关的条件几乎要按照琼剧来进行判断，最终选择放弃。

## 其他人的代码

```
def isMatch(self, s, p):
    m = len(s)
    n = len(p)
    dp = [[True] + [False] * m]
    for i in xrange(n):
        dp.append([False]*(m+1))
    
    for i in xrange(1, n + 1):
        x = p[i-1]
        if x == '*' and i > 1:
            dp[i][0] = dp[i-2][0]
        for j in xrange(1, m+1):
            if x == '*':
                dp[i][j] = dp[i-2][j] or dp[i-1][j] or (dp[i-1][j-1] and p[i-2] == s[j-1]) or (dp[i][j-1] and p[i-2]=='.')
            elif x == '.' or x == s[j-1]:
                dp[i][j] = dp[i-1][j-1]
    
    return dp[n][m]
```

## 总结

这份代码采用了动态规划，需要更多时间来消化。