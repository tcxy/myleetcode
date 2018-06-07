# Median of Two Sorted Arrays

## Description

There are two sorted arrays nums1 and nums2 of size m and n respectively.

Find the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).

## 思路

这题目的难点在于O(log (m+n))。如果是O(m+n)的话个人觉得可以新建一个数组来存储最后的结果，然后开始遍历数组A，在遍历数组A的时候可以用另一个值来表示数组B当前访问到第几个数了，然后数组A每访问一个数，根据A中的数和B中的数来判断哪个应该在前，以及B中的数是否要插入新的数组中。当然，这里还要判断一下数组中的最后一个数是多少，以免出现B中的某个数应该排在A中某几个数之后的情况。如果要O(log (m+n))的话基本上就是需要用到其他的方案的，而且还不能遍历完两个数组。最佳方法应该是分治了，主要还是得考虑中位数。因为前面的数小，后面的数大，并且位数还是数组正中间。最关键的问题就是A数组中的第i个元素和B数组中的第j个元素，使得i+j-2为两个数组长度和的一半。关键问题就在于如何求i和j的值。

## 方案一

```

class Solution(object):
    def findMedianSortedArrays(self, nums1, nums2):
        """
        :type nums1: List[int]
        :type nums2: List[int]
        :rtype: float
        """
        result_array = [] # Store all the number in num1 and num2, sorted
        length = 0 # Indicate how many numbers in result_array
        length1 = len(nums1) # The length of nums1
        length2 = len(nums2) # The length of nums2
        sub1 = 0 # Subscript for nums1
        sub2 = 0 # Subscript for nums2
        while sub1 != length1 or sub2 != length2:
            num1 = nums1[sub1] if sub1 <= length1 - 1 else float('inf')
            num2 = nums2[sub2] if sub2 <= length2 - 1 else float('inf')
            if num1 <= num2 or sub2 == length2:
                result_array.append(num1)
                sub1 += 1
            elif num2 < num1 or sub1 == length1:
                result_array.append(num2)
                sub2 += 1
            length += 1
        if length % 2 == 0:
            median = length / 2
            return (result_array[median - 1] + result_array[median]) / 2.0
        else:
            return result_array[length // 2]
```

问题在于O(m+n)

## 方案二

```

class Solution(object):
    def findMedianSortedArrays(self, nums1, nums2):
        """
        :type nums1: List[int]
        :type nums2: List[int]
        :rtype: float
        """
        len1 = len(nums1); len2 = len(nums2)
        if (len1 + len2) % 2 == 1: 
            return self.getKth(nums1, nums2, (len1 + len2) // 2 + 1)
        else:
            return (self.getKth(nums1, nums2, (len1 + len2) // 2) + self.getKth(nums1, nums2, (len1 + len2) // 2 + 1)) * 0.5
        
    def getKth(self, nums1, nums2, k):
        len1 = len(nums1)
        len2 = len(nums2)
        if len1 > len2: 
            return self.getKth(nums2, nums1, k)
        if len1 == 0: 
            return nums2[k - 1]
        if k == 1: 
            return min(nums1[0], nums2[0])
        p1 = min(k/2, len1)
        p2 = k - p1
        if nums1[p1 - 1] <= nums2[p2 - 1]:
            return self.getKth(nums1[p1:], nums2, p2)
        else:
            return self.getKth(nums1, nums2[p2:], p1)
```

### 具体思路

实际上，这题要求取得第k个值。为了节省时间，直接去两个数组的中位数，分别为m1和m2。如果m1小于m2，说明数组1中的前一半的数都是不需要的。这个时候直接从m1开始接着找，由于舍弃了数组1中一半的数，这个时候不再是求K，而是求k减去m1中舍弃的那一半的数。

## 方案三


这个方案是参照博客[两个有序数组中的中位数和Top K问题](https://blog.csdn.net/hk2291976/article/details/51107778)

这个方法的思路比较有意思，和方案二有点类似。同样是从取两个数组的中位数开始，但是这里采用了另一种方式来实现数组的变更，这一点和找最大回文序列类似。通过把数组的长度设置为2n+1，这样就会有两个下标对应同一个数字，也就是不需要担心奇偶问题。另外，这个方案中，将一个数组的取中位数的操作定义为割，并且不修改数组原本的值。相应的，如何更改取的值就成了问题。这里采用的方案是利用lo和hi，类似二分的形式，然后通过运算来修改lo和hi的值。为了简化操作，lo和hi都是在nums1上进行操作。同时，这里采用割的操作是同时在两个数组上进行并且需要利用割的位置两边的数来进行判断，也就是说，会存在数组1的割的位置的左和右以及数组2割的位置的左和右两种情况。

``` python

```

## 总结

可以说是写得非常波折了，这题目对于分治和递归的要求还是挺高的。