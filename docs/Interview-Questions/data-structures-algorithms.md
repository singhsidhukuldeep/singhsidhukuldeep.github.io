---
title: Data Structure and Algorithms
description: Data Structure and algorithms for cracking interviews
# hide:
#   - toc
---

# Data Structure and Algorithms (DSA)

![Total Questions](https://img.shields.io/badge/Total%20Questions-5-blue?style=flat&labelColor=black&color=blue)
![Unanswered Questions](https://img.shields.io/badge/Unanswered%20Questions-0-blue?style=flat&labelColor=black&color=yellow)
![Answered Questions](https://img.shields.io/badge/Answered%20Questions-5-blue?style=flat&labelColor=black&color=success)

[TOC]

## To-do :material-alert-decagram:{ .mdx-pulse title="Need Contributions 🤝" }

- [ ] Add https://leetcode.com/discuss/interview-question/344650/Amazon-Online-Assessment-Questions

<!---
|[Easy 😁](#easy) | [Medium 🙂](#medium) | [Hard 🤨](#hard) | [Very Hard 😲](#very-hard)|
|---|---|---|---|
|:-:|:-:|:-:|:-:|
-->

---

## 😁 Easy 

---

### Two Number Sum

!!! question 

	Write a function that takes in a non-empty array of distinct integers and an
	integer representing a target sum. 

	If any two numbers in the input array sum
	up to the target sum, the function should return them in an array, in any
	order. 

	If no two numbers sum up to the target sum, the function should return
	an empty array.

	??? example "Try it!"
		- LeetCode: https://leetcode.com/problems/two-sum/

	??? info "Hint 1"
		No Hint

	??? success "Answer"
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

### Validate Subsequence

!!! question 

	Given two non-empty arrays of integers, write a function that determines whether the second array is a subsequence of the first one.


	A subsequence of an array is a set of numbers that aren't necessarily adjacent in the array but that are in the same order as they appear in the array. For instance, the numbers [1, 3, 4]  form a subsequence of the array [1, 2, 3, 4] , and so do the numbers [2, 4].

	Note that a single number in an array and the array itself are both valid subsequences of the array.
	
	??? example "Try it!"
		- GeeksforGeeks: https://www.geeksforgeeks.org/problems/array-subset-of-another-array2317/1

	??? info "Hint 1"
		No Hint

	??? success "Answer"
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

### Nth Fibonacci

!!! question 

	The Fibonacci sequence is defined as follows:
	Any number in the sequence is the sum of the previous 2.

	for `fib[n] = fib[n-1] + fib[n-2]`

	The 1st and 2nd are fixed at 0,1

	Find the nth Nth Fibonacci sequence

	??? example "Try it!"
		- LeetCode: https://leetcode.com/problems/fibonacci-number/
		- GeeksforGeeks: https://www.geeksforgeeks.org/problems/nth-fibonacci-number1335/1


	??? info "Hint 1"
		No Hint

	??? success "Answer"
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

### Product Sum

!!! question 

	Write a function that takes in a "special" array and returns its product sum. A "special" array
	is a non-empty array that contains either integers or other "special" arrays. The product sum of a "special" array is the sum of its
	elements, where "special" arrays inside it are summed themselves and then multiplied by their level of depth.

	For example, the product sum of `[x, y]` is
	`x + y` ; the product sum of `[x, [y, z]]`
	is `x + 2y + 2z`

	Eg:
	Input: `[5, 2, [7, -1], 3, [6, [-13, 8], 4]]`
	Output: `12 # calculated as: 5 + 2 + 2 * (7 - 1) + 3 + 2 * (6 + 3 * (-13 + 8) + 4)`

	??? example "Try it!"
		- LeetCode: https://leetcode.com/problems/fibonacci-number/
		- GeeksforGeeks: https://www.geeksforgeeks.org/problems/nth-fibonacci-number1335/1

	??? info "Hint 1"
		No Hint

	??? success "Answer"

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

## 🙂 Medium 

---

### Top K Frequent Words

!!! question 

	Given a non-empty list of words, return the *k* most frequent elements.

	Your answer should be sorted by frequency from highest to lowest. If two words have the same frequency, then the word with the lower alphabetical order comes first.

	Example 1:

	```
	Input: ["i", "love", "leetcode", "i", "love", "coding"], k = 2
	Output: ["i", "love"]
	Explanation: "i" and "love" are the two most frequent words.
		Note that "i" comes before "love" due to a lower alphabetical order.
	```

	Example 2:

	```
	Input: ["the", "day", "is", "sunny", "the", "the", "the", "sunny", "is", "is"], k = 4
	Output: ["the", "is", "sunny", "day"]
	Explanation: "the", "is", "sunny" and "day" are the four most frequent words,
		with the number of occurrence being 4, 3, 2 and 1 respectively.
	```
	Note:

	1.  You may assume *k* is always valid, 1 ≤ *k* ≤ number of unique elements.
	2.  Input words contain only lowercase letters.

	Follow up:

	1.  Try to solve it in *O*(*n* log *k*) time and *O*(*n*) extra space.


	??? example "Try it!"
		- LeetCode: https://leetcode.com/problems/top-k-frequent-words/

	??? info "Hint 1"
		No Hint

	??? success "Answer"
		```Python
		# Count the frequency of each word, and 
		# sort the words with a custom ordering relation 
		# that uses these frequencies. Then take the best k of them.

		# Time Complexity: O(N \log{N})O(NlogN), where NN is the length of words. 
		# We count the frequency of each word in O(N)O(N) time, 
		# then we sort the given words in O(N \log{N})O(NlogN) time.
		# Space Complexity: O(N)O(N), the space used to store our uniqueWords.
		def topKFrequentWords(words, k)-> List[str]:
			from collections import Counter
			wordsFreq = Counter(words)
			uniqueWords = list(wordsFreq.keys())
			uniqueWords.sort(key = lambda x: (-wordsFreq[x], x))
			return uniqueWords[:k]
		```

		```Python
		# Time Complexity: O(N \log{k})O(Nlogk), where NN is the length of words. 
		# We count the frequency of each word in O(N)O(N) time, then we add NN words to the heap, 
		# each in O(\log {k})O(logk) time. Finally, we pop from the heap up to kk times. 
		# As k \leq Nk≤N, this is O(N \log{k})O(Nlogk) in total.

		# In Python, we improve this to O(N + k \log {N})O(N+klogN): our heapq.heapify operation and 
		# counting operations are O(N)O(N), and 
		# each of kk heapq.heappop operations are O(\log {N})O(logN).

		# Space Complexity: O(N)O(N), the space used to store our wordsFreq.

		# Count the frequency of each word, then add it to heap that stores the best k candidates. 
		# Here, "best" is defined with our custom ordering relation, 
		# which puts the worst candidates at the top of the heap. 
		# At the end, we pop off the heap up to k times and reverse the result 
		# so that the best candidates are first.

		# In Python, we instead use heapq.heapify, which can turn a list into a heap in linear time, 
		# simplifying our work.

		def topKFrequentWords(words, k)-> List[str]:
			from heapq import heapify, heappop#, heappush
			from collections import Counter
			wordsFreq = Counter(words)
			heap = [(-freq, word) for word, freq in wordsFreq.items()]
			heapq.heapify(heap)
			return [heapq.heappop(heap)[1] for _ in range(k)]
		```

## 🤨 Hard 

---


---

## 😲 Very Hard 

---


---