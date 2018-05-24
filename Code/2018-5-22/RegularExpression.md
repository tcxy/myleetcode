# Regular Expression Matching

## description

Given an input string (s) and a pattern (p), implement regular expression matching with support for '.' and '*'.

## 思路

主要参考动态规划的答案来看的，这里的动态规划采用了一个二维数组来存放结果。这个数组是m+1 x n + 1的，m是s的长度，n是p的长度。m+1意味着从0开始到字符串长度为止的匹配结果，bp\[i + 1\]\[j + 1\]意味着s[0..i]和p[0..j]的匹配结果。对于b[i+1][0]来说，其值一定是False，因为匹配的是空串。对于bp[0][j+1]来说，其值为 j > 0  and '*' == p[j] and b[0][j - 1]，对于第二个值来说，第一个值是True，所以主要看第二个值是不是*，因为第二个值为\*的时候有可能是空串对空匹配，这样也是成立的。如果匹配串是由多个带\*的字符构成，俺么主要就是看前两个位置是否为\*来判断。以上属于边界情况，正常递推的时候，主要看当前字符是否为\*。如果不是，那么b[i+1][j+1] = b[i][j] and ('.' == p[j] or s[i] == p[j])，简单点说就是，在第i位置的时候要看看前一个位置是不是匹配上了。当前字符是\*的时候，b[i + 1][j + 1] = b[i + 1][j - 1] and j > 0 or b[i + 1][j] or b[i][j + 1] and j > 0 and ('.' == p[j - 1] or s[i] == p[j - 1])。当出现\*的时候，有三种情况可以考虑。一是这个字符不出现，二是出现一次，三是出现多次。根据这三种情况需要一一做判断，比如前一个字符是否能够匹配，或者前两个字符（\*对应字符不出现）。以及当前字符能不能匹配。

## 代码

``` python
class Solution:
    def isMatch(self, s, p):
        m = len(s)
        n = len(p)
        dp = [[True] + [False] * m]
        for i in range(n):
            dp.append([False]*(m+1))

        for i in range(1, n + 1):
            x = p[i-1]
            if x == '*' and i > 1:
                dp[i][0] = dp[i-2][0]
            for j in range(1, m+1):
                if x == '*':
                    dp[i][j] = dp[i-2][j] or dp[i-1][j] or (dp[i-1][j-1] and p[i-2] == s[j-1]) or (dp[i][j-1] and p[i-2]=='.')
                elif x == '.' or x == s[j-1]:
                    dp[i][j] = dp[i-1][j-1]

        return dp[n][m]
```

## 总结

DP的公式非常难以推导，尤其是在参数较多的时候。这题看起来有点无从下手，但是实际上，每次的比较都是基于字符来进行。也就是存在两个参数，再加上\*的判断条件非常麻烦。由于结果只是看能否匹配，所以主要是看\*在三种不同匹配的情况下怎么走。另外，由于这个匹配的特性，基本上只能按照自顶向下的方法来进行。