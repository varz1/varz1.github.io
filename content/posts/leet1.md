---
title: "leetcode算法day1-双指针"
date: 2021-02-22T21:38:48+08:00
description: 双指针训练
---

## 1. 两数之和 II - 输入有序数组

给定一个已按照 **升序排列** 的整数数组 `numbers` ，请你从数组中找出两个数满足相加之和等于目标数 `target` 。

函数应该以长度为 `2` 的整数数组的形式返回这两个数的下标值*。*`numbers` 的下标 **从 1 开始计数** ，所以答案数组应当满足 `1 <= answer[0] < answer[1] <= numbers.length` 。

你可以假设每个输入只对应唯一的答案，而且你不可以重复使用相同的元素。

**示例 1：**

```
输入：numbers = [2,7,11,15], target = 9
输出：[1,2]
解释：2 与 7 之和等于目标数 9 。因此 index1 = 1, index2 = 2 。
```

**示例 2：**

```
输入：numbers = [2,3,4], target = 6
输出：[1,3]
```

双指针解法

```go
func twoSum(numbers []int, target int) []int {
	l := len(numbers)
	for i, j:= 0, l-1; i < j; {
		sum := numbers[i] + numbers[j]
		if sum == target {
			return []int{i+1, j+1}
		} else if sum < target {
			i++
		} else {
			j--
		}
	}
	return []int{}
}
```

思路：使用双指针遍历数组，左为小指针右为大指针。条件判断和小移动左指针，和大移动右指针。

##  2.平方数之和

633. Sum of Square Numbers (Easy)

[Leetcode](https://leetcode.com/problems/sum-of-square-numbers/description/) / [力扣](https://leetcode-cn.com/problems/sum-of-square-numbers/description/)

```
Input: 5
Output: True
Explanation: 1 * 1 + 2 * 2 = 5
```

题目描述：判断一个非负整数是否为两个整数的平方和。

```go
func judgeSquareSum(target int) bool {
	c := float64(target)
	for i, j := 0, int(math.Sqrt(c)); i <= j; {
		sum := i*i+j*j
		if sum == int(c){
			return true
		}else if sum < int(c){
			i++
		}else {
			j--
		}
	}
	return false
}
```

，思路：类似1。需注意右指针设为目标数的根号。

## 3. 反转字符串中的元音字符

345. Reverse Vowels of a String (Easy)

[Leetcode](https://leetcode.com/problems/reverse-vowels-of-a-string/description/) / [力扣](https://leetcode-cn.com/problems/reverse-vowels-of-a-string/description/)

```
Given s = "leetcode", return "leotcede".
```
```go
func reverseVowels(s string) string {
	word := make([]byte, len(s))
	for i := 0; i < len(s); i++ {
		word[i] = s[i]
	}
	for i, j := 0, len(s)-1;i < j; {
		if isInclude(s[i]) && isInclude(s[j]) {
			word[i], word[j] = s[j], s[i]
			i++
			j--
		}
		if !isInclude(s[i]) {
			i++
		}
		if !isInclude(s[j]) {
			j--
		}
	}
	return string(word)
}

func isInclude(c byte) bool {
	return c == 'a' || c=='e' || c=='i' || c=='o' || c=='u' ||c == 'A' || c=='E' || c=='I' || c=='O' || c=='U'
}
```

思路：使用双指针遍历，头尾相等即交换位置不相等先移动前指针后移动后指针。

## 4. 回文字符串

680. Valid Palindrome II (Easy)

[Leetcode](https://leetcode.com/problems/valid-palindrome-ii/description/) / [力扣](https://leetcode-cn.com/problems/valid-palindrome-ii/description/)

```
Input: "abca"
Output: True
Explanation: You could delete the character 'c'.
```

题目描述：可以删除一个字符，判断是否能构成回文字符串。

所谓的回文字符串，是指具有左右对称特点的字符串，例如 "abcba" 就是一个回文字符串。

```go
func validPalindrome(s string) bool {
	for i, j := 0, len(s)-1; i < j; {
		if s[i] != s[j] {
			return isPalindrome(s[i:j]) || isPalindrome(s[i+1:j+1])
		}
		i++
		j--
	}
	return true
}

func isPalindrome(s string) bool {
	i := 0
	j := len(s) - 1
	for i < j {
		if s[i] != s[j] {
			return false
		}
		i++
		j--
	}
	return true
}
```

思路：使用双指针可以很容易判断一个字符串是否是回文字符串：令一个指针从左到右遍历，一个指针从右到左遍历，这两个指针同时移动一个位置，每次都判断两个指针指向的字符是否相同，如果都相同，字符串才是具有左右对称性质的回文字符串。

## 5. 归并两个有序数组

88. Merge Sorted Array (Easy)

[Leetcode](https://leetcode.com/problems/merge-sorted-array/description/) / [力扣](https://leetcode-cn.com/problems/merge-sorted-array/description/)

```
Input:
nums1 = [1,2,3,0,0,0], m = 3
nums2 = [2,5,6],       n = 3

Output: [1,2,2,3,5,6]
```

题目描述：把归并结果存到第一个数组上。

```go
func merge(nums1 []int, m int, nums2 []int, n int) {
	for i, j := 0, m; i < n; i++ {
		nums1[j] = nums2[i]
		j++
	}
	sort.Ints(nums1)
}
```

思路：首先将nums2数组元素添加到nums1后面然后利用sort函数进行排序

## 6. 判断链表是否存在环

141. Linked List Cycle (Easy)

[Leetcode](https://leetcode.com/problems/linked-list-cycle/description/) / [力扣](https://leetcode-cn.com/problems/linked-list-cycle/description/)

```go
func hasCycle(head *ListNode) bool {
	if head != nil {
		slow := head
		fast := head
		for fast != nil && fast.Next != nil {
			slow = slow.Next
			fast = fast.Next.Next
			if slow == fast {
				return true
			}
		}
	}
	return false
}
```

思路：使用双指针，满指针每次移动一个节点，快指针每次移动两个节点，如果存在环，那么这两个指针一定会相遇。

## 7. 最长子序列

524. Longest Word in Dictionary through Deleting (Medium)

[Leetcode](https://leetcode.com/problems/longest-word-in-dictionary-through-deleting/description/) / [力扣](https://leetcode-cn.com/problems/longest-word-in-dictionary-through-deleting/description/)

```
Input:
s = "abpcplea", d = ["ale","apple","monkey","plea"]

Output:
"apple"
```

题目描述：删除 s 中的一些字符，使得它构成字符串列表 d 中的一个字符串，找出能构成的最长字符串。如果有多个相同长度的结果，返回字典序的最小字符串。

```go
func findLongestWord(s string, d []string) string {
	LongestWord := ""
	for _, str := range d {
		l1, l2 := len(LongestWord), len(str)
		if l1 > l2 || (l1 == l2 && strings.Compare(LongestWord, str) < 0) {
			continue
		}
		if isOk(s, str) {
			LongestWord = str
		}
	}
	return LongestWord
}

func isOk(s string, t string) bool {
	var i, j = 0, 0
	for i < len(s) && j < len(t) {
		if s[i] == t[j] {
			j++
		}
		i++
	}
	return j == len(t)
}
```

思路：isOK函数双指针判断是否为子序列，for循环判断是否最长字串
