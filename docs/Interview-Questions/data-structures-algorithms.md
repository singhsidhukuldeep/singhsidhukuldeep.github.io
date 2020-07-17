---
title: Data Structure and Algorithms
description: Data Structure and algorithms for cracking interviews
---

# Data Structure and Algorithms (DSA)

![Total Questions](https://img.shields.io/badge/Total%20Questions-4-blue?style=flat&labelColor=black&color=blue)
![Unanswered Questions](https://img.shields.io/badge/Unanswered%20Questions-0-blue?style=flat&labelColor=black&color=yellow)
![Answered Questions](https://img.shields.io/badge/Answered%20Questions-4-blue?style=flat&labelColor=black&color=success)

## Easy

* [Two Number Sum](#two-number-sum)
* [Validate Subsequence](#validate-subsequence)
* [Nth Fibonacci](#nth-fibonacci)
* [Product Sum](#product-sum)

## Medium

## Hard

## Very Hard

##
---
##

## Two Number Sum

Write a function that takes in a non-empty array of distinct integers and an
integer representing a target sum. 

If any two numbers in the input array sum
up to the target sum, the function should return them in an array, in any
order. 

If no two numbers sum up to the target sum, the function should return
an empty array.

```Python
# O(n) time | O(n) space
def twoNumberSum(array, targetSum):
	avail = set()
	for i,v in enumerate(array):
		if targetSum-v in avail:
			return [targetSum-v,v]
		else:
			avail.add(v)
	return []
    pass
```
```Python
# O(nlog(n)) time | O(1) space
def twoNumberSum(array, targetSum):
	array.sort()
	n = len(array)
	left = 0
	right = n-1
	while left<right:
		currSum = array[left]+array[right]
		if currSum==targetSum: return [array[left], array[right]]
		elif currSum<targetSum: left+=1
		elif currSum>targetSum: right-=1
	return []
    pass
```
```Python
# O(n^2) time | O(1) space
def twoNumberSum(array, targetSum):
    n = len(array)
	for i in range(n-1):
		for j in range(i+1,n):
			if array[i]+array[j] == targetSum:
				return [array[i],array[j]]
	return []
    pass
```

---

## Validate Subsequence

Given two non-empty arrays of integers, write a function that determines whether the second array is a subsequence of the first one.


A subsequence of an array is a set of numbers that aren't necessarily adjacent in the array but that are in the same order as they appear in the array. For instance, the numbers [1, 3, 4]  form a subsequence of the array [1, 2, 3, 4] , and so do the numbers [2, 4].

Note that a single number in an array and the array itself are both valid subsequences of the array.

```Python
# O(n) time | O(1) space - where n is the length of the array
def isValidSubsequence(array, sequence):
    pArray = pSequence = 0
	while pArray < len(array) and pSequence < len(sequence):
		if array[pArray] == sequence[pSequence]:
			pArray+=1
			pSequence+=1
		else: pArray+=1
	return pSequence == len(sequence)
    pass
```

---

## Nth Fibonacci

The Fibonacci sequence is defined as follows:
Any number in the sequence is the sum of the previous 2.

for `fib[n] = fib[n-1] + fib[n-2]`

The 1st and 2nd are fixed at 0,1

Find the nth Nth Fibonacci sequence


```Python
# O(n) time | O(n) space
def getNthFib(n):
    dp = [0,1]
	while len(dp)<n:
		dp.append(dp[-1]+dp[-2])
	return dp[n-1]
    pass
```

```Python
# O(n) time | O(1) space
def getNthFib(n):
    last_two = [0,1]
	count = 2
	while count < n:
		currFib = last_two[0] + last_two[1]
		last_two[0] = last_two[1]
		last_two[1] = currFib
		count += 1
	return last_two[1] if n>1 else last_two[0]
    pass
```

---

## Product Sum

Write a function that takes in a "special" array and returns its product sum. A "special" array
is a non-empty array that contains either integers or other "special" arrays. The product sum of a "special" array is the sum of its
elements, where "special" arrays inside it are summed themselves and then multiplied by their level of depth.

For example, the product sum of `[x, y]` is
`x + y` ; the product sum of `[x, [y, z]]`
is `x + 2y + 2z`

Eg:
Input: `[5, 2, [7, -1], 3, [6, [-13, 8], 4]]`
Output: `12 # calculated as: 5 + 2 + 2 * (7 - 1) + 3 + 2 * (6 + 3 * (-13 + 8) + 4)`

```Python
# O(n) time | O(d) space - where n is the total number of elements in the array,
# including sub-elements, and d is the greatest depth of "special" arrays in the array
def productSum(array, depth = 1):
    sum = 0
	for i,v in enumerate(array):
		if type(v) is list:
			sum += productSum(v, depth + 1)
		else:
			sum += v
	return sum*depth
    pass
```

---