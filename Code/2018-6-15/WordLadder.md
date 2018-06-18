# Word Ladder

## Description

Given two words (beginWord and endWord), and a dictionary's word list, find the length of shortest transformation sequence from beginWord to endWord, such that:

1. Only one letter can be changed at a time.
2. Each transformed word must exist in the word list. Note that beginWord is not a transformed word.

## 思路

主要是BFS的题目，参考了一下这个博客。[Word Ladder](https://www.jianshu.com/p/753bd585d57e)

## 代码

``` python
class Solution(object):
    def ladderLength(self, beginWord, endWord, wordList):
        """
        :type beginWord: str
        :type endWord: str
        :type wordList: List[str]
        :rtype: int
        """
        wordList = list(set(wordList)) 
        visited = set() 
        visited.add(beginWord)
        dist = 1 
        while endWord not in visited: 
            temp = set() 
            for word in visited: 
                for unvisit in wordList[:]:
                    diff = 0
                    for i in range(len(word)):
                        if word[i] != unvisit[i]:
                            diff += 1
                    if diff == 1:
                        wordList.remove(unvisit)
                        temp.add(unvisit)
            dist += 1 
            if len(temp) == 0: # if 0, it never gets to the endWord 
                return 0 
            visited = temp 
        return dist
```

这个方案超时

## 代码2

``` python
class Solution(object): 
    def ladderLength(self, beginWord, endWord, wordList): 
        """ :type beginWord: str
        :type endWord: str
        :type wordList: List[str]
        :rtype: int
        """
        wordList = set(wordList)
        visited = set()
        visited.add(beginWord)  
        dist = 1
        while endWord not in visited:
            temp = set()
            for word in visited:
                for i in range(len(word)):
                    chars = list(word)
                    for j in range(ord('a'), ord('z') + 1):
                        chars[i] = chr(j)
                        newWord = ''.join(chars)
                        if newWord in wordList:
                        temp.add(newWord)
                        wordList.remove(newWord)
            dist += 1 
            if len(temp) == 0:
                return 0
            visited = temp
        return dist
```

这个方案可以提交，但是速度不太理想。

## 代码3

``` python
class Solution(object):
    def ladderLength(self, beginWord, endWord, wordList):
        """
        :type beginWord: str
        :type endWord: str
        :type wordList: List[str]
        :rtype: int
        """
        def construct_word(wordList):
            d = {}
            for word in wordList:
                for i in range(len(word)):
                    s = word[:i] + "_" + word[i+1:]
                    d[s] = d.get(s, []) + [word]
            return d
        def bfs(beginWord, endWord, wordList):
            queue, visited = [[beginWord, 1]], set()
            while queue:
                word, step = queue.pop(0)
                if word not in visited:
                    visited.add(word)
                    if word == endWord:
                        return step
                    for i in range(len(word)):
                        s = word[:i] + "_" + word[i+1:]
                        words = wordList.get(s, [])
                        for neighbor in words:
                            if neighbor not in visited:
                                queue.append([neighbor, step + 1])
            return 0
        return bfs(beginWord, endWord, construct_word(wordList))
```

这个方案通过自行构建表缩短了寻找的时间。

## 扩展

双向BFS