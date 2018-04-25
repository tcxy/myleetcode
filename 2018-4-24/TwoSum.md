# Two Sum

## Problem description

Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

## 思路

不需要考虑无解问题，所以直接考虑怎么获取结果。target的值获取之后，可以直接通过双重循环来遍历整个数组，然后比较结果是否为target。
同时也不需要考虑有多个解的问题，所以只需要考虑一个结果即可。


## 方案一

'''

def twoSum(self, nums, target):
	for index1, value1 in enumerate(nums):
		for index2, value2 in enumerate(nums):
			if index1 != index2 and num1 + num2 == target:
				return index1, index2
	# If no solution
	return -1

'''

### 问题

执行到最后一个sample的时候出现超时了，最后这一个sample确实有点变态，数组中的东西太多，Python的双重循环无法通过可能与python运行效率有关。

### 思路

最大的问题应该是双重循环，需要相办法用一个循环解决问题。
主要目的是在访问到每一个元素的时候不需要访问所有的元素，比如1+3不等于target，这样访问到3的时候就不需要再考虑1了。
这个思路需要用到两个数组，本质上来说其实还是和之前双重循环差不多，但是备用数组的数据是可以删除的，比如1走完了没有target那就直接从备用数组中删除1。
复杂度应该是O(nlogn)，但是并没有解决双重循环的问题。

## 方案二

'''
def twoSum(self, nums, target):
	start_index = 1 # use one number to denote how many elements have been valued
	for index1, value1 in enumerate(nums):
		for index2 in range(start_index, len(nums)):
			if value1 + nums[index2] == target:
				return index1, index2
		start_index = start_index + 1 # We've valued this element
	# If we can't find the right answer
	return -1

'''

### 总结

这次成功通过，基本上时间是优化得差不多了，不过不知道能不能优化到O(nlogn)的程度

## O(n)

discussion有人给出O(n)的解法

'''

def twoSum(self, nums, target):
	if len(nums) <= 1:
		return False
	buff_dict = {}
	for i in range(len(nums)):
		if nums[i] in buff_dict:
			return [buff_dict[nums[i]], i]
		else:
			buff_dict[target - nums[i]] = i
'''

基本上是反向了一波，每访问一个num的时候考虑的点是target-num。
利用字典的键值对来存储值和其所需要的值的下标，这样可以直接寻找字典中是否存在要找的值。
这个方案有所考虑，但是因为感觉避不过双重循环就没有继续下去，实际来说，因为哈希表的访问速度，所以这种方案虽然看起来像是要遍历两边，实际上字典寻找值的时候复杂度为O(1)。