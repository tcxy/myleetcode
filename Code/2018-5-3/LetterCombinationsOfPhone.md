# Letter Combinations of a Phone Number

## Description

Given a string containing digits from 2-9 inclusive, return all possible letter combinations that the number could represent.

A mapping of digit to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.

## 思路

这题基本没什么思路，如果直接采用列举的话，指数级的时间复杂度，肯定超时。不过我试了下，居然还真的可以直接列举，除了有一个为空的时候需要判断之外倒是没什么。除此之外我能想到的就只有递归了，通过递归来不停地求后面的字符。


## 列举

```
class Solution:
    def letterCombinations(self, digits):
        """
        :type digits: str
        :rtype: List[str]
        """
        if len(digits) == 1:
            return []
        dict = {"1":"", "2":"abc", "3":"def", "4":"ghi", "5":"jkl", "6":"mno", "7":"pqrs","8":"tuv","9":"wxyz","10":" "}
        result = [""]
        for digit in digits:
            lst = dict[digit]
            newresult = []
            for char in lst:
                for str in result:
                    newresult.append(str+char)
            result = newresult
        return result
```

## 总结

虽然这题过了，但是我觉得靠列举或者递归应该都不算非常好的方案。有空还是要找找这题有没有什么更加巧妙地算法。