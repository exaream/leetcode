# Easy Level Problems

- https://leetcode.com/problemset/all/?page=1&difficulty=EASY
- https://leetcode.com/explore/interview/card/top-interview-questions-easy/

## 2235. Add Two Integers

- https://leetcode.com/problems/add-two-integers/
- `Math`
- Runtime 2 ms, Memory 1.9 MB
```go
func sum(num1 int, num2 int) int {
	return num1 + num2
}
```


## 1480. Running Sum of 1d Array

- https://leetcode.com/problems/running-sum-of-1d-array/
- `Array` `Prefix Sum`
- Runtime 8 ms, Memory 2.8 MB
```go
func runningSum(nums []int) []int {
	length := len(nums)
	ans := make([]int, length)
	ans[0] = nums[0]

	for i := 1; i < length; i++ {
		ans[i] = nums[i] + ans[i-1]
	}

	return ans
}
```


## 1672. Richest Customer Wealth

- https://leetcode.com/problems/richest-customer-wealth/
- `Array` `Matrix`
- Runtime 7 ms, Memory 3.1 MB
```go
func maximumWealth(accounts [][]int) int {
	max := 0

	for _, customer := range accounts {
		cur := 0
		for _, amount := range customer {
			cur += amount
		}
		if cur > max {
			max = cur
		}
	}

	return max
}
```

## 412. Fizz Buzz

- https://leetcode.com/problems/fizz-buzz/
- `Math` `String` `Simulation`
- Runtime 11 ms, Memory 3.6 MB
```go
func fizzBuzz(n int) []string {
	ans := make([]string, n)

	for i := 1; i <= n; i++ {
		var str string

		if i%3 == 0 {
			str += "Fizz"
		}
		if i%5 == 0 {
			str += "Buzz"
		}
		if str == "" {
			str = strconv.Itoa(i)
		}

		ans[i-1] = str
	}

	return ans
}
```


## 1342. Number of Steps to Reduce a Number to Zero

- https://leetcode.com/problems/number-of-steps-to-reduce-a-number-to-zero/
- `Math` `Bit Manipulation`
- Runtime 4 ms, Memory 1.9 MB
```go
func numberOfSteps(num int) int {
	if num <= 0 {
		return 0
	}

	ans := 0
	for num > 0 {
		if num%2 == 0 {
			num /= 2
		} else {
			num--
		}

		ans++
	}

	return ans
}
```

- Runtime 0 ms, Memory 1.8 MB
```go
func numberOfSteps(num int) int {
	if num == 0 {
		return 0
	}

	ans := 0
	for num > 0 {
		ans += num&1 + 1
		num >>= 1
	}

	return ans - 1
}
```


## 876. Middle of The Linked List

- https://leetcode.com/problems/middle-of-the-linked-list/
- `Linked List` `Two Pointers`
- Runtime 0 ms, Memoery 2.1 MB
```go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func middleNode(head *ListNode) *ListNode {
	list := make([]*ListNode, 0)

	for head != nil {
		list = append(list, head)
		head = head.Next
	}

	return list[len(list)/2]
}
```

- Runtime 3 ms, Memoery 2 MB
```go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func middleNode(head *ListNode) *ListNode {
	middle, end := head, head

	for end != nil && end.Next != nil {
		middle = middle.Next
		end = end.Next.Next
	}

	return middle
}
```


## 383. Ransom Note

- https://leetcode.com/problems/ransom-note/
- `Hash Table` `String` `Counting`
- Runtime 7 ms, Memory 3.8 MB
```go
func canConstruct(ransomNote string, magazine string) bool {
	alphabet := make([]int, 26)

	for _, v := range magazine {
		alphabet[v-'a']++
	}

	for _, v := range ransomNote {
		if alphabet[v-'a'] == 0 {
			return false
		}
		alphabet[v-'a']--
	}

	return true
}
```


## 1. Two Sum

- https://leetcode.com/problems/two-sum/
- `Array` `Hash Table`
- brute force
- Runtime 33 ms, Memory 3.5 MB
```go
func twoSum(nums []int, target int) []int {
	for i := 0; i < len(nums); i++ {
		for j := i + 1; j < len(nums); j++ {
			if nums[i]+nums[j] == target {
				return []int{i, j}
			}
		}
	}

	return nil
}
```

- hashmap
- Runtime 0 ms, Memory 4.3 MB
```go
func twoSum(nums []int, target int) []int {
	m := make(map[int]int)

	for idxA, num := range nums {
		if idxB, ok := m[target-num]; ok {
			return []int{idxB, idxA}
		}
		m[num] = idxA
	}

	return nil
}
```

## 1704. Determine if String Halves Are Alike

- https://leetcode.com/problems/determine-if-string-halves-are-alike/
- `String` `Counting`
- Runtime 0ms, Memory 2.2MB
```go
func halvesAreAlike(s string) bool {
	cnt := 0
	half := len(s) / 2

	for _, v := range []string{"a", "e", "i", "o", "u", "A", "E", "I", "O", "U"} {
		cnt += strings.Count(s[:half], v)
		cnt -= strings.Count(s[half:], v)
	}

	return cnt == 0
}
```

## 13. Roman to Integer

- https://leetcode.com/problems/roman-to-integer/
- `Hash Table` `Math` `String`
- Runtime 19 ms, Memory 2.9 MB
```go
func romanToInt(s string) int {
	m := map[byte]int{'I': 1, 'V': 5, 'X': 10, 'L': 50, 'C': 100, 'D': 500, 'M': 1000}
	length := len(s)
	total := 0

	for i := 0; i < length; {
		if (i+1 < length) && (m[s[i]] < m[s[i+1]]) {
			total += m[s[i+1]] - m[s[i]]
			i += 2
		} else {
			total += m[s[i]]
			i += 1
		}
	}

	return total
}
```

- Runtime 8 ms, Memory 2.9 MB
```go
func romanToInt(s string) int {
	m1 := map[string]int{"I": 1, "V": 5, "X": 10, "L": 50, "C": 100, "D": 500, "M": 1000}
	m2 := map[string]int{"IV": 4, "IX": 9, "XL": 40, "XC": 90, "CD": 400, "CM": 900}
	length := len(s)
	total := 0

	for i := 0; i < length; {
		// 2 letters
		if (i+1 < length) && m2[s[i:i+2]] != 0 {
			total += m2[s[i:i+2]]
			i += 2
		} else {
			total += m1[s[i:i+1]]
			i += 1
		}
	}

	return total
}
```


## 14. Longest Common Prefix

- https://leetcode.com/problems/longest-common-prefix/
- `String`
- Runtime 0 ms, Memory 2.4 MB
```go
func longestCommonPrefix(strs []string) string {
	ans := strs[0]

	for _, str := range strs[1:] {
		i := 0
		for ; i < len(str) && i < len(ans) && ans[i] == str[i]; i++ {
		}
		ans = ans[:i]
	}

	return ans
}
```


## 20. Valid Parentheses

- https://leetcode.com/problems/valid-parentheses/
- `String` `Stack`
- Runtime 0 ms, Memory 2 MB
```go
func isValid(s string) bool {
	stack := make([]rune, 0)
	pairs := map[rune]rune{
		')': '(',
		']': '[',
		'}': '{',
	}

	for _, char := range s {
		switch char {
		case '(', '{', '[':
			stack = append(stack, char)
		case ')', '}', ']':
			if len(stack) == 0 || stack[len(stack)-1] != pairs[char] {
				return false
			}
			stack = stack[:len(stack)-1]
		}
	}

	return len(stack) == 0
}
```


## 21. Merge Two Sorted Lists

- https://leetcode.com/problems/merge-two-sorted-lists/
- `Linked List` `Recursion`
- Runtime 0 ms, Memory 2.5 MB
```go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func mergeTwoLists(list1 *ListNode, list2 *ListNode) *ListNode {
	head := &ListNode{}
	cur := head

	for list1 != nil && list2 != nil {
		if list1.Val < list2.Val {
			cur.Next = list1
			list1 = list1.Next
		} else {
			cur.Next = list2
			list2 = list2.Next
		}
		cur = cur.Next
	}

	if list1 != nil {
		cur.Next = list1
	}
	if list2 != nil {
		cur.Next = list2
	}

	return head.Next
}
```


## 26. Remove Duplicates from Sorted Array

- https://leetcode.com/problems/remove-duplicates-from-sorted-array/
- `Array` `Two Pointers`
- Runtime 7 ms, Memory 4.3 MB
```go
func removeDuplicates(nums []int) int {
	length := len(nums)
	if length <= 1 {
		return length
	}

	slow := 0
	for fast := 1; fast < length; fast++ {
		if nums[slow] != nums[fast] {
			slow++
			nums[slow] = nums[fast]
		}
	}

	// for i := slow + 1; i < len(nums); i++ {
	// 	nums[i] = 0
	// }
	// fmt.Println(nums)

	return slow + 1
}
```


## 121. Best Time to Buy and Sell Stock

- https://leetcode.com/problems/best-time-to-buy-and-sell-stock/
- `Array` `Dynamic Programming`
- Runtime 179 ms, Memory 9 MB
```go
func maxProfit(prices []int) int {
	max := 0
	min := prices[0]

	for i := 1; i < len(prices); i++ {
		min = int(math.Min(float64(prices[i]), float64(min)))
		max = int(math.Max(float64(prices[i]-min), float64(max)))
	}

	return max
}
```

- Runtime 158 ms, Memory 9.4 MB
```go
func maxProfit(prices []int) int {
	max := 0
	min := prices[0]

	for i := 1; i < len(prices); i++ {
		if prices[i] < min {
			min = prices[i]
		}
		if prices[i]-min > max {
			max = prices[i] - min
		}
	}

	return max
}
```


## 66. Plus One

- https://leetcode.com/problems/plus-one/
- `Array` `Math`
- Runtime 0 ms, Memory 2.1 MB
```go
func plusOne(digits []int) []int {
	for i := len(digits) - 1; i >= 0; i-- {
		if digits[i] < 9 {
			digits[i] += 1
			return digits
		}
		digits[i] = 0
	}

	// If all digits are 9,
	return append([]int{1}, digits...)
	// The above line is the same as below.

	// digits = append(digits, 0)
	// digits[0] = 1
	// return digits
}
```


## 283. Move Zeroes

- https://leetcode.com/problems/move-zeroes/
- `Array` `Two Pointers`
- Runtime 26 ms, Memory 6.6 MB
```go
func moveZeroes(nums []int) {
	idx := 0
	for i := 0; i < len(nums); i++ {
		if nums[i] == 0 {
			continue
		}
		nums[i], nums[idx] = nums[idx], nums[i]
		idx++
	}
}
```


## 217. Contains Duplicate

- https://leetcode.com/problems/contains-duplicate/
- `Array` `Hash Table` `Sorting`
- Runtime 155 ms, Memory 8.5 MB
```go
func containsDuplicate(nums []int) bool {
	sort.Ints(nums)

	for i := 1; i < len(nums); i++ {
		if nums[i] == nums[i-1] {
			return true
		}
	}

	return false
}
```

- Runtime 70 ms, Memory 8.6 MB
```go
func containsDuplicate(nums []int) bool {
	m := make(map[int]bool)

	for i := 0; i < len(nums); i++ {
		if m[nums[i]] {
			return true
		}
		m[nums[i]] = true
	}

	return false
}
```


## 136. Single Number

- https://leetcode.com/problems/single-number/
- `Array` `Bit Manipulation`
- Runtime 18 ms, Memory 6.7 MB
```go
func singleNumber(nums []int) int {
	m := make(map[int]bool)

	for i := range nums {
		if _, ok := m[nums[i]]; ok {
			m[nums[i]] = false
            continue
		}
		m[nums[i]] = true
	}

	ans := 0
	for k, v := range m {
		if v {
			ans = k
			break
		}
	}

	return ans
}
```

- `ans = ans ^ v` was faster than `ans ^= v`
- Runtime 13 ms, Memory 6.2 MB
```go
func singleNumber(nums []int) int {
	ans := 0
	for _, v := range nums {
		ans = ans ^ v
	}
	return ans
}
```


## 349. Intersection of Two Arrays

- https://leetcode.com/problems/intersection-of-two-arrays/
- `Array` `Hash Table` `Two Pointers` `Binary Search` `Sorting`
- Runtime 5 ms, Memory 2.8 MB
```go
func intersection(nums1 []int, nums2 []int) []int {
	m := make(map[int]struct{}, 0)

	for i := 0; i < len(nums1); i++ {
		for j := 0; j < len(nums2); j++ {
			if nums1[i] == nums2[j] {
				m[nums1[i]] = struct{}{}
				break
			}
		}
	}

	ans := make([]int, 0)
	for k, _ := range tmp {
		ans = append(ans, k)
	}

	return ans
}
```

- Runtime 4 ms, Memory 3 MB
```go
func intersection(nums1 []int, nums2 []int) []int {
	m := make(map[int]bool)

	for _, v := range nums1 {
		m[v] = true
	}

	ans := make([]int, 0)
	for _, v := range nums2 {
		if m[v] {
			ans = append(ans, v)
			m[v] = false
		}
	}

	return ans
}
```


## 350. Intersection of Two Arrays II

- https://leetcode.com/problems/intersection-of-two-arrays-ii/
- `Array` `Hash Table` `Two Pointers` `Binary Search` `Sorting`
- Runtime 0 ms, Memory 3 MB
```go
func intersect(nums1 []int, nums2 []int) []int {
	cnt := make(map[int]int, len(nums1))
	for _, v := range nums1 {
		cnt[v]++
	}

	var ans []int
	for _, v := range nums2 {
		if cnt[v] == 0 {
			continue
		}
		ans = append(ans, v)
		cnt[v]--
	}

	return ans
}
```


## 344. Reverse String

- https://leetcode.com/problems/reverse-string/
- `Two Pointers` `String`
- Runtime 47 ms, Memory 6.6 MB
```go
func reverseString(s []byte) {
	for i, j := 0, len(s)-1; i < j; i, j = i+1, j-1 {
		s[i], s[j] = s[j], s[i]
	}
}
```


## 242. Valid Anagram

- https://leetcode.com/problems/valid-anagram/
- `Hash Table` `String` `Sorting`
- Runtime 3 ms, Memory 2.7 MB
```go
func isAnagram(s string, t string) bool {
	lenS, lenT := len(s), len(t)
	if lenS != lenT {
		return false
	}
	cnt := make([]int, 26)
	for i := 0; i < lenT; i++ {
		cnt[s[i]-'a']++
		cnt[t[i]-'a']--
	}
	for i := 0; i < 26; i++ {
		if cnt[i] != 0 {
			return false
		}
	}
	return true
}
```


## 125. Valid Palindrome

- https://leetcode.com/problems/valid-palindrome/
- `Two Pointers` `String`
- Runtime 20 ms, Memory 6 MB
```go
func isPalindrome(s string) bool {
	s = strings.ToLower(s)
	s = regexp.MustCompile(`[^a-z0-9]+`).ReplaceAllString(s, "")
	fmt.Println(s)
	list := strings.Split(s, "")

	for i, j := 0, len(list)-1; i < j; i, j = i+1, j-1 {
		if list[i] != list[j] {
			return false
		}
	}

	return true
}
```

- Runtime 4 ms, Memory 3.1 MB
```go
func isPalindrome(s string) bool {
	list := make([]rune, 0, len(s))

	for _, c := range s {
		if 'a' <= c && c <= 'z' || '0' <= c && c <= '9' {
			list = append(list, c)
		} else if 'A' <= c && c <= 'Z' {
			list = append(list, 'a'+(c-'A'))
		}
	}

	length := len(list)

	for i, c := range list[:length/2] {
		if c != list[length-i-1] {
			return false
		}
	}
```


## 206. Reverse Linked List

- https://leetcode.com/problems/reverse-linked-list/
- `Linked List` `Recursion`
- Runtime 6 ms, Memory 2.6 MB
```go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func reverseList(head *ListNode) *ListNode {
	var pre *ListNode
	cur := head
	for cur != nil {
		cur, pre, cur.Next = cur.Next, cur, pre
	}
	return pre
}
```

- Runtime 3 ms, Memory 2.5 MB
```go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func reverseList(head *ListNode) *ListNode {
	var prev, cur, next *ListNode = nil, head, nil

	for cur != nil {
		next = cur.Next
		cur.Next = prev
		prev = cur
		cur = next
	}

	return prev
}
```


## 234. Palindrome Linked List

- https://leetcode.com/problems/palindrome-linked-list/
-  `Linked List`,  `Two Pointers`,  `Stack`,  `Recursion`
- Runtime 323 ms, Memory 12.1 MB
```go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func isPalindrome(head *ListNode) bool {
	stack := make([]int, 0, 100000)
	for node := head; node != nil; i = node.Next {
		stack = append(stack, node.Val)
	}

	i := len(stack)/2 - 1
	j := len(stack) / 2
	if len(stack)%2 == 1 {
		j++
	}

	for i >= 0 && j <= len(stack)-1 {
		if stack[i] != stack[j] {
			return false
		}
		i--
		j++
	}

	return true
}
```

- Runtime 142 ms, Memory 10.4 MB
```go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func isPalindrome(head *ListNode) bool {
	cur := head
	var stack []int
	for cur != nil {
		stack = append(stack, cur.Val)
		cur = cur.Next
	}

	for i, j := 0, len(stack)-1; i < j; i, j = i+1, j-1 {
		if stack[i] != stack[j] {
			return false
		}
	}

	return true
}
```


## 141. Linked List Cycle

- https://leetcode.com/problems/linked-list-cycle/
- `Hash Table`,  `Linked List`,  `Two Pointers`
- Runtime 24 ms, Memory 6.7 MB
```go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func hasCycle(head *ListNode) bool {
	stack := make(map[*ListNode]int, 0)
	cur := head

	for cur != nil {
		if _, ok := stack[cur]; ok {
			return true
		}
		stack[cur]++
		cur = cur.Next
	}

	return false
}
```

- Runtime 19 ms, Memory 4.4 MB
```go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func hasCycle(head *ListNode) bool {
	slow, fast := head, head
	for fast != nil && fast.Next != nil {
		slow = slow.Next
		fast = fast.Next.Next
		if slow == fast {
			return true
		}
	}
	return false
}
```


## 104. Maximum Depth of Binary Tree

- https://leetcode.com/problems/maximum-depth-of-binary-tree/
- `Tree`,  `Depth-First Search`,  `Breadth-First Search`,  `Binary Tree`
- Runtime 2 ms, Memory 4.1 MB
```go
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func maxDepth(root *TreeNode) int {
	if root == nil {
		return 0
	}
	return max(maxDepth(root.Left), maxDepth(root.Right)) + 1
}

func max(x int, y int) int {
	if x > y {
		return x
	}
	return y
}
```


## 101. Symmetric Tree

- https://leetcode.com/problems/symmetric-tree/
-  `Tree`,  `Depth-First Search`,  `Breadth-First Search` `Binary Tree`
-  Runtime 0 ms, Memory 2.8 MB
```go
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func isSymmetric(root *TreeNode) bool {
	return isMirror(root.Left, root.Right)
}

func isMirror(left, right *TreeNode) bool {
	if left == nil && right == nil {
		return true
	}
	if left == nil || right == nil {
		return false
	}
	if left.Val != right.Val {
		return false
	}
	return isMirror(left.Left, right.Right) && isMirror(left.Right, right.Left)
}
```


## 108. Convert Sorted Array to Binary Search Tree

- https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/
- `Array` `Divide and Conquer` `Tree` `Binary Search Tree` `Binary Tree`
- Runtime 6 ms, Memory 3.5 MB
```go
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func sortedArrayToBST(nums []int) *TreeNode {
	switch len(nums) {
	case 0:
		return nil
	case 1:
		return &TreeNode{Val: nums[0]}
	}

	mid := len(nums) / 2
	return &TreeNode{
		Val:   nums[mid],
		Left:  sortedArrayToBST(nums[:mid]),
		Right: sortedArrayToBST(nums[mid+1:]),
	}
}
```


## 88. Merge Sorted Array

- https://leetcode.com/problems/merge-sorted-array/
- `Array` `Two Pointers` `Sorting`
- Runtime 3 ms, Memory 2.3 MB
```go
func merge(nums1 []int, m int, nums2 []int, n int) {
	nums1 = append(nums1[:m], nums2[:n]...)
	sort.Ints(nums1)
}
```

- Runtime 0 ms, Memory 2.3 MB
```go
func merge(nums1 []int, m int, nums2 []int, n int) {
	im := m - 1
	in := n - 1
	i := n + m - 1 // Putting this in the for clause makes this function slower than it is now.

	for ; i >= 0 && in >= 0; i-- {
		if nums1[i] == 0 { // Using != to apply Early Return makes this function slower than it is now.
			if im >= 0 && nums1[im] > nums2[in] {
				nums1[im], nums1[i] = nums1[i], nums1[im]
				im--
			} else {
				nums1[i] = nums2[in]
				in--
			}
		}
	}
}
```


## 278. First Bad Version

- https://leetcode.com/problems/first-bad-version/
- `Binary Search` `Interactive`
- Runtime 0 ms, Memory 2 MB

```go
/** 
 * Forward declaration of isBadVersion API.
 * @param   version   your guess about first bad version
 * @return 	 	      true if current version is bad 
 *			          false if current version is good
 * func isBadVersion(version int) bool;
 */
func firstBadVersion(end int) int {
	start := 1
	for start < end {
		mid := start + int((end-start)/2)
		if isBadVersion(mid) {
			end = mid
		} else {
			start = mid + 1
		}
		if start == end {
			break
		}
	}
	return start
}
```


## 70. Climbing Stairs

- https://leetcode.com/problems/climbing-stairs/
- `Dynamic Programming` `Memoization`
- Runtime 1 ms, Memory 1.9 MB

```go
// Pattern from 1 to 3
// 1 --> 1 way:  1
// 2 --> 2 ways: 2-1-1
// 3 --> 3 ways: 1-1-1 || 1-2 || 2-1
func climbStairs(n int) int {
	// Fibonacci
	cur, next := 1, 2
	for i := 2; i < n+1; i++ {
		cur, next = next, cur+next
	}
	return cur
}
```


## 326. Power of Three

- https://leetcode.com/problems/power-of-three/
- `Math` `Recursion`
- Runtime 59 ms, Memory 6.5 MB
```go
func isPowerOfThree(n int) bool {
	if n < 1 {
		return false
	}

	for n%3 == 0 {
		n /= 3
	}

	return n == 1
}
```

- Runtime 59 ms, Memory 6.5 MB
```go
func isPowerOfThree(n int) bool {
	if n < 1 {
		return false
	}
	if n%3 == 0 {
		return isPowerOfThree(n / 3)
	}
	if n == 1 {
		return true
	}
	return false
}
```


## 191. Number of 1 Bits

- https://leetcode.com/problems/number-of-1-bits/
- `Divide and Conquer` `Bit Manipulation`
- Runtime 0 ms, Memory 2 MB
```go
func hammingWeight(num uint32) int {
	ans := 0
	str := strconv.FormatUint(uint64(num), 2)
	for _, v := range str {
		if v == '1' {
			ans++
		}
	}
	return ans
}
```

- Runtime 0 ms, Memory 1.9 MB
- `num = num >> 1` is faster than `num >>= 1`.
```go
func hammingWeight(num uint32) int {
	var ans uint32

	for num != 0 {
		ans += num & 1
		num = num >> 1
	}

	return int(ans)
}
```

- Runtime 0 ms, Memory 1.8 MB
```go
func hammingWeight(num uint32) int {
	return bits.OnesCount32(num)
}
```


## 461. Hamming Distance

- https://leetcode.com/problems/hamming-distance/
- `Bit Manipulation`
- Runtime 3 ms, Memory 1.9 MB
```go
func hammingDistance(x int, y int) int {
	ans := 0
	xor := x ^ y

	for xor > 0 {
		xor = xor & (xor - 1)
		ans++
	}

	return ans
}
```

- Runtime 2 ms, Memory 2 MB
```go
func hammingDistance(x int, y int) int {
	return strings.Count(fmt.Sprintf("%b", x^y), "1")
}
```

- Runtime 0 ms, Memory 2 MB
```go
func hammingDistance(x int, y int) int {
	return bits.OnesCount(uint(x^y))
}
```

- Runtime 0 ms, Memory 2 MB
```go
func hammingDistance(x int, y int) int {
	ans := 0
	bin := fmt.Sprintf("%b", x^y)
	for i := 0; i < len(bin); i++ {
		if rune(bin[i]) == '1' {
			ans++
		}
	}
	return ans
}
```


## 190. Reverse Bits

- https://leetcode.com/problems/reverse-bits/
- `Divide and Conquer` `Bit Manipulation`
- Runtime 0 ms, Memory 2.6 MB
- `num = num >> 1` is faster than `num >>= 1`.
```go
func reverseBits(num uint32) uint32 {
	var ans uint32
	for i := 0; i < 32; i++ {
		ans = ans<<1 + num&1
		num = num >> 1
	}
	return ans
}
```


## 118. Pascal's Triangle

- https://leetcode.com/problems/pascals-triangle/
- `Array` `Dynamic Programming`
- Runtime 0 ms, Memory 2.1 MB
```go
func generate(numRows int) [][]int {
	var ans [][]int

	for i := 0; i < numRows; i++ {
		row := make([]int, i+1)
		row[0], row[i] = 1, 1
		for j := 0; j <= i; j++ {
			if row[j] == 0 {
				row[j] = ans[i-1][j-1] + ans[i-1][j]
			}
		}
		ans = append(ans, row)
	}

	return ans
}
```

## 268. Missing Number

- https://leetcode.com/problems/missing-number/
- `Array` `Hash Table` `Math` `Binary Search` `Bit Manipulation`
- Runtime 35 ms, Memory 6.4 MB
```go
func missingNumber(nums []int) int {
	length := len(nums)
	total := length * (length + 1) / 2

	for _, i := range nums {
		total -= i
	}

	return total
}
```

- Runtime 17 ms, Memory 6.5 MB
```go
func missingNumber(nums []int) int {
	length := len(nums)
	r := nums[0]
	for i := 1; i < length; i++ {
		r ^= (i ^ nums[i])
	}
	r ^= length
	return r
}
```


## 202. Happy Number

- https://leetcode.com/problems/happy-number/
- `Hash Table` `Math` `Two Pointers`
- Runtime 0 ms, Memory 1.9 MB
```go
func isHappy(n int) bool {
	slow, fast := n, n

	for {
		slow = calc(slow)
		fast = calc(calc(fast))
		if slow == fast {
			break
		}
	}

	if slow == 1 {
		return true
	}

	return false
}

// Calculate square digit sum.
func calc(n int) int {
	sum := 0
	for n > 0 {
		tmp := n % 10
		sum += tmp * tmp
		n /= 10

	}
	return sum
}
```


## 171. Excel Sheet Column Number

- https://leetcode.com/problems/excel-sheet-column-number/
- `Math` `String`
- Runtime 0 ms, Memory 2.1 MB
```go
func titleToNumber(s string) int {
	ans := 0
	for i := 0; i < len(s); i++ {
		ans *= 26
		ans += int(s[i]-'A') + 1
	}
	return ans
}
```


## 69. Sqrt(x)

- https://leetcode.com/problems/sqrtx/
- `Math` `Binary Search`
- Runtime 0 ms, Memory 2.1 MB
```go
func mySqrt(x int) int {
	if x <= 1 {
		return x
	}

	low, high := 1, x

	for low < high-1 {
		mid := (low + high + 1) / 2
		if mid*mid == x {
			return mid
		}
		if mid*mid > x {
			high = mid
		} else {
			low = mid
		}
	}

	return low
}
```


## 94. Binary Tree Inorder Traversal

- https://leetcode.com/problems/binary-tree-inorder-traversal/
- `Stack` `Tree` `Depth-First Search` `Binary Tree`
- Runtime 0 ms, Memory 2 MB

```go
func inorderTraversal(root *TreeNode) []int {
	if root == nil {
		return nil
	}
	ans := inorderTraversal(root.Left)
	ans = append(ans, root.Val)
	ans = append(ans, inorderTraversal(root.Right)...)
	return ans
}
```


## 160. Intersection of Two Linked Lists

- https://leetcode.com/problems/intersection-of-two-linked-lists/
- `Hash Table` `Linked List` `Two Pointers`
- Runtime 74ms, Memory 7.5 MB
```go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func getIntersectionNode(headA, headB *ListNode) *ListNode {
	if headA == nil || headB == nil {
		return nil
	}
	hasVisited := make(map[*ListNode]struct{})

	for n := headA; n != nil; n = n.Next {
		hasVisited[n] = struct{}{}
	}

	for n := headB; n != nil; n = n.Next {
		if _, ok := hasVisited[n]; ok {
			return n
		}
	}
	return nil
}
```

- Runtime 35 ms, Memory 7.1 MB
```go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func getIntersectionNode(headA, headB *ListNode) *ListNode {
	curA, curB := headA, headB
	lenA, lenB := 0, 0
	for curA != nil {
		curA = curA.Next
		lenA++
	}
	for curB != nil {
		curB = curB.Next
		lenB++
	}

	var count int
	var fast, slow *ListNode
	if lenA > lenB {
		fast, slow = headA, headB
		count = lenA - lenB
	} else {
		fast, slow = headB, headA
		count = lenB - lenA
	}

	for fast != nil && slow != nil {
		// Skip if there is a difference in the number of 2 nodes 
		// before they intersect.
		if count > 0 {
			fast = fast.Next
			count--
			continue
		}
		if fast == slow {
			return fast
		}
		fast = fast.Next
		slow = slow.Next
	}
	return fast
}
```


## 169. Majority Element

- https://leetcode.com/problems/majority-element/
- `Array` `Hash Table` `Divide and Conquer` `Sorting` `Counting`
- Runtime 29 ms, Memory 7.1 MB
```go
func majorityElement(nums []int) int {
	std := len(nums) / 2
	cnt := make(map[int]int)
	for _, v := range nums {
		cnt[v]++
		if cnt[v] > std {
			return v
		}
	}
	return -1
}
```

- Runtime 22 ms, Memory 6 MB
```go
func majorityElement(nums []int) (result int) {
	sort.Ints(nums)
	return nums[len(nums)/2]
}
```

- Runtime 17 ms, Memory 6 MB
```go
func majorityElement(nums []int) int {
	cnt, candidate := 0, -1
	for i := 0; i < len(nums); i++ {
		if cnt == 0 {
			candidate = nums[i]
		}
		if candidate == nums[i] {
			cnt++
		} else {
			cnt--
		}
	}
	return candidate
}
```


## 387. First Unique Character in a String

- https://leetcode.com/problems/first-unique-character-in-a-string/
- `Hash Table` `String` `Queue` `Counting`
- Runtime 38 ms, Memory 5.4 MB

```go
func firstUniqChar(s string) int {
	cnt := make(map[byte]int)
	for i := 0; i < len(s); i++ {
		cnt[s[i]]++
	}
	for i := 0; i < len(s); i++ {
		if cnt[s[i]] == 1 {
			return i
		}
	}
	return -1
}
```

- Runtime 3 ms, Memory 5.2 MB
```go
func firstUniqChar(s string) int {
	m := make([]int, 26)
	for _, v := range s {
		m[v-'a']++
	}
	for i, v := range s {
		if m[v-'a'] == 1 {
			return i
		}
	}
	return -1
}
```


## 226. Invert Binary Tree

- https://leetcode.com/problems/invert-binary-tree/
- `Tree` `Depth-First Search` `Breadth-First Search` `Binary Tree`
- Runtime 2 ms, Memory 2.1 MB
```go
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func invertTree(root *TreeNode) *TreeNode {
	if root == nil {
		return nil
	}
	root.Left, root.Right = invertTree(root.Right), invertTree(root.Left)
	return root
}
```


## 543. Diameter of Binary Tree

- https://leetcode.com/problems/diameter-of-binary-tree/
- `Tree` `Depth-First Search` `Binary Tree`
- Runtime 3 ms, Memory 4.3 MB
```go
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func diameterOfBinaryTree(root *TreeNode) int {
	ans := 0
	depth(root, &ans)
	return ans
}

func depth(root *TreeNode, ans *int) int {
	if root == nil {
		return 0
	}
	left := depth(root.Left, ans)
	right := depth(root.Right, ans)
	*ans = max(*ans, left+right)
	return max(left, right) + 1
}

func max(a, b int) int {
	if a > b {
		return a
	}
	return b
}
```


## 35. Search Insert Position

- https://leetcode.com/problems/search-insert-position/
- `Array` `Binary Search`
- Runtime 0 ms, Memory 3 MB
```go
func searchInsert(nums []int, target int) int {
	i := 0
	for i < len(nums) {
		if nums[i] >= target {
			return i
		}
		i++
	}
	return i
}
```


## 232. Implement Queue using Stacks

- https://leetcode.com/problems/implement-queue-using-stacks/
- `Stack` `Design` `Queue`
- Runtime 0 ms, Memory 1.9 MB
```go
type MyQueue struct {
	stack []int
}

func Constructor() MyQueue {
	return MyQueue{}
}

func (m *MyQueue) Push(x int) {
	m.stack = append(m.stack, x)
}

func (m *MyQueue) Pop() int {
    first := m.stack[0]
	m.stack = m.stack[1:]
	return first
}

func (m *MyQueue) Peek() int {
	return m.stack[0]
}

func (m *MyQueue) Empty() bool {
	return len(m.stack) == 0
}
```


## 27. Remove Element

- https://leetcode.com/problems/remove-element/
- `Array` `Two Pointers`
- Runtime 5 ms, Memory 2.1 MB
```go
func removeElement(nums []int, val int) int {
	for i := 0; i < len(nums); i++ {
		if val == nums[i] {
			nums = append(nums[:i], nums[i+1:]...)
			i--
		}
	}
	return len(nums)
}
```

- Runtime 0 ms, Memory 2.1 MB
```go
func removeElement(nums []int, val int) int {
	ans := 0
	for i := 0; i < len(nums); i++ {
		if nums[i] != val {
			nums[ans] = nums[i]
			ans++
		}
	}
	return ans
}
```


## 58. Length of Last Word

- https://leetcode.com/problems/length-of-last-word/
- `String`
- Runtime 2 ms, Memory 2 MB
```go
func lengthOfLastWord(s string) int {
	words := strings.Fields(s)
	return utf8.RuneCountInString(words[len(words)-1])
}
```

- Runtime 0 ms, Memory 2.1 MB
```go
func lengthOfLastWord(s string) int {
	s = strings.Trim(s, " ")
	words := strings.Split(s, " ")
	return len(words[len(words)-1])
}
```


## 205. Isomorphic Strings

- https://leetcode.com/problems/isomorphic-strings/
- `Hash Table` `String`
- Runtime 6 ms, Memory 2.6 MB
```go
func isIsomorphic(s string, t string) bool {
	ptnS, ptnT := map[byte]int{}, map[byte]int{}

	for i := range s {
		if ptnS[s[i]] != ptnT[t[i]] {
			return false
		} else {
			ptnS[s[i]] = i + 1
			ptnT[t[i]] = i + 1
		}
	}

	return true
}
```


## 119. Pascal's Triangle II

- https://leetcode.com/problems/pascals-triangle-ii/
- `Array` `Dynamic Programming`
- Runtime 2 ms, Memory 2.1 MB
```go
func getRow(rowIndex int) []int {
	row := []int{1}
	for r := 0; r < rowIndex; r++ {
		next := make([]int, r+2)
		for i := range row {
			next[i] += row[i]
			next[i+1] += row[i]
		}
		row = next
	}
	return row
}
```

- Runtime 2 ms, Memory 2 MB
```go
func getRow(rowIndex int) []int {
	ans := make([]int, 0)

	for i := 0; i <= rowIndex; i++ {
		tmp := make([]int, len(ans))
		copy(tmp, ans)
		ans = append(ans, 1)
		for j := 1; j < len(ans)-1; j++ {
			ans[j] = tmp[j-1] + tmp[j]
		}
	}

	return ans
}
```

- Runtime 0 ms, Memory 2.2 MB
```go
func getRow(rowIndex int) []int {
	if rowIndex == 0 {
		return []int{1}
	}
	prev := getRow(rowIndex - 1)
	ans := []int{1}
	for i := 1; i < len(prev); i++ {
		ans = append(ans, prev[i-1]+prev[i])
	}
	return append(ans, 1)
}
```


## 389. Find the Difference

- https://leetcode.com/problems/find-the-difference/
- `Hash Table` `String` `Bit Manipulation` `Sorting`
- Runtime 2 ms, Memory 2.2 MB
```go
func findTheDifference(s string, t string) byte {
	listS := []byte(s)
	listT := []byte(t)
	ans := listT[len(t)-1]

	for i, _ := range listS {
		ans += listT[i] - listS[i]
	}

	return ans
}
```

- Runtime 0 ms, Memory 3 MB
```go
func findTheDifference(s string, t string) byte {
	m := make(map[rune]int, len(s))
	for _, r := range s {
		m[r]++
	}
	for _, r := range t {
		if m[r] == 0 {
			return byte(r)
		}
		m[r]--
	}
	return 0
}
```


## 409. Longest Palindrome

- https://leetcode.com/problems/longest-palindrome/
- `Hash Table` `String` `Greedy`
- Runtime 0 ms, Memory 2 MB
```go
func longestPalindrome(s string) int {
	cnt := make(map[rune]int, 26)
	for _, r := range s {
		cnt[r]++
	}

	ans := 0
	odd := false
	for _, n := range cnt {
		if n%2 == 0 {
			ans += n
		} else {
			ans += n - 1
			odd = true
		}
	}

	if odd {
		ans++
	}

	return ans
}
```


## 100. Same Tree

- https://leetcode.com/problems/same-tree/
- `Tree` `Depth-First Search` `Breadth-First Search` `Binary Tree`
- Runtime 1 ms, Memory 2 MB
```go
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func isSameTree(p *TreeNode, q *TreeNode) bool {
	if p == nil && q == nil {
		return true
	}

	if p == nil || q == nil {
		return false
	}

	if p.Val != q.Val {
		return false
	}

	return isSameTree(p.Right, q.Right) && isSameTree(p.Left, q.Left)
}
```


## 111. Minimum Depth of Binary Tree

- https://leetcode.com/problems/minimum-depth-of-binary-tree/
- `Tree` `Depth-First Search` `Breadth-First Search` `Binary Tree`
- Runtime 177 ms, Memory 17.6 MB
```go
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func minDepth(root *TreeNode) int {
	queue := []*TreeNode{root}
	counter := 0
	n := len(queue)

	for n != 0 {
		counter++

		for i := 0; i < n; i++ {
			node := queue[0]
			queue = queue[1:]
			if node != nil {
				if node.Left == nil && node.Right == nil {
					return counter
				}
				queue = append(queue, node.Left)
				queue = append(queue, node.Right)
			}
		}

		n = len(queue)
	}

	return 0
}
```


## 112. Path Sum

- https://leetcode.com/problems/path-sum/
- `Tree` `Depth-First Search` `Breadth-First Search` `Binary Tree`
- Runtime 4 ms, Memory 4.6 MB
```go
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func hasPathSum(root *TreeNode, targetSum int) bool {
	if root == nil {
		return false
	}
	if root.Val == targetSum && root.Left == nil && root.Right == nil {
		return true
	}
	targetSum -= root.Val
	return hasPathSum(root.Left, targetSum) || hasPathSum(root.Right, targetSum)
}
```


## 367. Valid Perfect Square

- https://leetcode.com/problems/valid-perfect-square/
- `Math` `Binary Search`
- Runtime 0 ms, Memory 1.9 MB
```go
func isPerfectSquare(num int) bool {
	left, right := 1, num

	for left <= right {
		middle := (left + right) / 2
		square := middle * middle

		if square == num {
			return true
		}

		if square > num {
			right = middle - 1
		} else if square < num {
			left = middle + 1
		}
	}

	return false
}
```

- If you can use math.Sqrt() in this solution
- Runtime 0 ms, Memory 1.8 MB
```go
func isPerfectSquare(num int) bool {
	sqrt := math.Sqrt(float64(num))
	_, frac := math.Modf(sqrt)
	return frac == 0
}
```


## 463. Island Perimeter

- https://leetcode.com/problems/island-perimeter/
- `Array` `Depth-First Search` `Breadth-First Search` `Matrix`
- Runtime 44 ms, Memory 6.9 MB
```go
func islandPerimeter(grid [][]int) int {
	rows := len(grid)
	cols := len(grid[0])
	ans := 0

	for y := 0; y < rows; y++ {
		for x := 0; x < cols; x++ {
			if grid[y][x] != 1 {
				continue
			}
			if x == 0 || grid[y][x-1] == 0 { // left
				ans++
			}
			if x == cols-1 || grid[y][x+1] == 0 { // right
				ans++
			}
			if y == 0 || grid[y-1][x] == 0 { // above
				ans++
			}
			if y == rows-1 || grid[y+1][x] == 0 { // bottom
				ans++
			}
		}
	}

	return ans
}
```


## 2236. Root Equals Sum of Children

- https://leetcode.com/problems/root-equals-sum-of-children/
- `Tree` `Binary Tree`
- Runtime 3 ms, Memory 2 MB
```go
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func checkTree(root *TreeNode) bool {
	return root.Val == (root.Left.Val + root.Right.Val)
}
```


## 2367. Number of Arithmetic Triplets

- https://leetcode.com/problems/number-of-arithmetic-triplets/
- `Array` `Hash Table` `Two Pointers` `Enumeration`
- Runtime 2 ms, Memory 2.1 MB
```go
func arithmeticTriplets(nums []int, diff int) int {
	tmp := make([]bool, 201)
	for _, num := range nums {
		tmp[num] = true
	}

	ans := 0
	for _, num := range nums {
		if num+diff*2 <= 200 {
			if tmp[num+diff] && tmp[num+diff*2] {
				ans++
			}
		}
	}

	return ans
}
```
- Runtime 0 ms, Memory 2.1 MB
```go
func arithmeticTriplets(nums []int, diff int) int {
	ans := 0

	for i := 0; i < len(nums); i++ {
		for j := i + 1; j < len(nums); j++ {
			if nums[j]-nums[i] == diff {
				for k := j + 1; k < len(nums); k++ {
					if nums[k]-nums[j] == diff {
						ans++
					}
				}
			}
		}
	}

	return ans
}
```


## 1720. Decode XORed Array

- https://leetcode.com/problems/decode-xored-array/
- `Array` `Bit Manipulation`
- Runtime 31 ms, Memory 6.8 MB
```go
func decode(encoded []int, first int) []int {
	ans := make([]int, len(encoded)+1)
	ans[0] = first
	for i, v := range encoded {
		ans[i+1] = ans[i] ^ v
	}
	return ans
}
```
- Runtime 25 ms, Memory 6.8 MB
```go
func decode(encoded []int, first int) []int {
	ans := make([]int, len(encoded)+1)
	ans[0] = first
	for i := 1; i <= len(encoded); i++ {
		ans[i] =  ans[i-1] ^ encoded[i-1]
	}
	return ans
}
```


## 1614. Maximum Nesting Depth of the Parentheses

- https://leetcode.com/problems/maximum-nesting-depth-of-the-parentheses/
- `String` `Stack`
- Runtime 0 ms, Memory 1.8 MB
```go
func maxDepth(s string) int {
	cnt := 0
	ans := 0

	for i := range s {
		if s[i] == '(' {
			cnt++
		} else if s[i] == ')' {
			cnt--
		}

		ans = max(ans, cnt)
	}

	return ans
}

func max(a, b int) int {
	if a > b {
		return a
	}
	return b
}
```
- Runtime 0 ms, Memory 1.8 MB
```go
func maxDepth(s string) int {
	ans, cnt := 0, 0

	for _, r := range s {
		switch r {
		case rune('('):
			cnt++
		case rune(')'):
			cnt--
		}

		if cnt > ans {
			ans = cnt
		}
	}

	return ans
}
```


## 1464. Maximum Product of Two Elements in an Array

- https://leetcode.com/problems/maximum-product-of-two-elements-in-an-array/
- `Array` `Sorting` `Heap (Priority Queue)`
- Runtime 3 ms, Memory 2.9 MB
```go
func maxProduct(nums []int) int {
	sort.Ints(nums)
	length := len(nums)
	return (nums[length-1] - 1) * (nums[length-2] - 1)
}
```
- Runtime 0 ms, Memory 2.9 MB
```go
func maxProduct(nums []int) int {
	max, second := nums[0], 0

	for i := 1; i < len(nums); i++ {
		if nums[i] > max {
			second = max
			max = nums[i]
		} else if nums[i] >= second {
			second = nums[i]
		}
	}

	return (max - 1) * (second - 1)
}
```


## 1791. Find Center of Star Graph

- https://leetcode.com/problems/find-center-of-star-graph/
- `Graph`
- Runtime 122 ms, Memory 15.3 MB
```go
func findCenter(edges [][]int) int {
	m := make(map[int]bool, 2)

	for _, v := range edges {
		if m[v[0]] {
			return v[0]
		}
		if m[v[1]] {
			return v[1]
		}

		m[v[0]], m[v[1]] = true, true
	}

	return -1
}
```
- Runtime 116 ms, Memory 13.8 MB
```go
func findCenter(edges [][]int) int {
	m := make(map[int]struct{}, 2)

	for _, v := range edges {
		if _, ok := m[v[0]]; ok {
			return v[0]
		}
		if _, ok := m[v[1]]; ok {
			return v[1]
		}

		m[v[0]], m[v[1]] = struct{}{}, struct{}{}
	}

	return -1
}
```


## 1603. Design Parking System

- https://leetcode.com/problems/design-parking-system/
- `Design` `Simulation` `Counting`
- Runtime 47 ms, Memory 7.1 MB
```go
const (
	Big = iota + 1
	Medium
	Small
)

type ParkingSystem struct {
	slots map[int]int
}

func Constructor(big int, medium int, small int) ParkingSystem {
	return ParkingSystem{
		slots: map[int]int{Big: big, Medium: medium, Small: small},
	}
}

func (ps *ParkingSystem) AddCar(carType int) bool {
	if ps.slots[carType] > 0 {
		ps.slots[carType]--
		return true
	}
	return false
}

/**
 * Your ParkingSystem object will be instantiated and called as such:
 * obj := Constructor(big, medium, small);
 * param_1 := obj.AddCar(carType);
 */
```

- Runtime 35 ms, Memory 7.2 MB
```go
const (
	Big = iota + 1
	Medium
	Small
)

type ParkingSystem struct {
	space    map[int]int
	occupied map[int]int
}

func Constructor(big int, medium int, small int) ParkingSystem {
	return ParkingSystem{
		space:    map[int]int{Big: big, Medium: medium, Small: small},
		occupied: map[int]int{Big: 0, Medium: 0, Small: 0},
	}
}

func (ps *ParkingSystem) AddCar(carType int) bool {
	if ps.occupied[carType] >= ps.space[carType] {
		return false
	} else {
		ps.occupied[carType]++
		return true
	}
}
```


## 1656. Design an Ordered Stream

- https://leetcode.com/problems/design-an-ordered-stream/
- `Array` `Hash Table` `Design` `Data Stream`
- Runtime 66 ms, Memory 7.3 MB
```go
type OrderedStream struct {
	ptr   int
	stack map[int]string
}

func Constructor(n int) OrderedStream {
	return OrderedStream{
		ptr:   0,
		stack: make(map[int]string, n),
	}
}

func (o *OrderedStream) Insert(idKey int, value string) []string {
	var ans []string
	o.stack[idKey-1] = value
	for o.stack[o.ptr] != "" {
		ans = append(ans, o.stack[o.ptr])
		o.ptr++
	}
	return ans
}

/**
 * Your OrderedStream object will be instantiated and called as such:
 * obj := Constructor(n);
 * param_1 := obj.Insert(idKey,value);
 */
 ```

## 1588. Sum of All Odd Length Subarrays

- https://leetcode.com/problems/sum-of-all-odd-length-subarrays/
- `Array` `Math` `Prefix Sum`
- Runtime 0 ms, Memory 2.1 MB
```go
func sumOddLengthSubarrays(a []int) int {
	ans := 0
	length := len(a)

	for i := 1; i <= length; i += 2 {
		for j := 0; (j + i) <= length; j++ {
			for _, v := range a[j : j+i] {
				ans += v
			}
		}
	}

	return ans
}
```


## 1920. Build Array from Permutation

- https://leetcode.com/problems/build-array-from-permutation/
- `Array` `Simulation`
- Runtime 14 ms, Memory 6.4 MB
```go
func buildArray(nums []int) []int {
	ans := make([]int, len(nums))
	for i, v := range nums {
		ans[i] = nums[v]
	}
	return ans
}
```


## 1863. Sum of All Subset XOR Totals

- https://leetcode.com/problems/sum-of-all-subset-xor-totals/
- `Array` `Math` `Backtracking` `Bit Manipulation` `Combinatorics`
- Runtime 2 ms, Memory 1.9 MB
```go
func subsetXORSum(nums []int) int {
	return dfs(nums, 0, 0)
}

// depth-first search
func dfs(nums []int, i int, xorSum int) int {
	if i == len(nums) {
		return xorSum
	}
	return dfs(nums, i+1, xorSum) + dfs(nums, i+1, xorSum^nums[i])
}
```
- Runtime 0 ms, Memory 2.8 MB
```go
func subsetXORSum(nums []int) int {
	return backtrack(nums, 0, make([]int, 0), 0)
}

func backtrack(nums []int, pos int, list []int, ans int) int {
	ans += xorSum(list)

	for i := pos; i < len(nums); i++ {
		list = append(list, nums[i])
		ans = backtrack(nums, i+1, list, ans)
		list = list[:len(list)-1]
	}

	return ans
}

func xorSum(list []int) int {
	sum := 0
	for i := 0; i < len(list); i++ {
		sum ^= list[i]
	}
	return sum
}
```


## 1512. Number of Good Pairs

- https://leetcode.com/problems/number-of-good-pairs/
- `Array` `Hash Table` `Math` `Counting`
- Runtime 1 ms, Memory 2 MB
```go
func numIdenticalPairs(nums []int) int {
	m := make(map[int]int)
	for _, v := range nums {
		m[v]++
	}

	ans := 0
	for _, v := range m {
		ans += v * (v - 1) / 2
	}

	return ans
}
```
- Runtime 1 ms, Memory 1.9 MB
```go
func numIdenticalPairs(nums []int) int {
	ans := 0
	for i := 0; i < len(nums)-1; i++ {
		for j := i + 1; j < len(nums); j++ {
			if nums[i] == nums[j] && i < j {
				ans++
			}
		}
	}

	return ans
}
```


## 1876. Substrings of Size Three with Distinct Characters

- https://leetcode.com/problems/substrings-of-size-three-with-distinct-characters/
- `Hash Table` `String` `Sliding Window` `Counting`
- Runtime 0 ms, Memory 2 MB
```go
func countGoodSubstrings(s string) int {
	ans := 0
	for i := 0; i < len(s)-2; i++ {
		alpha := make([]byte, 26)
		ok := true
		for _, v := range s[i : i+3] {
			alpha[v-'a']++
			if alpha[v-'a'] > 1 {
				ok = false
				break
			}
		}
		if ok {
			ans++
		}
	}

	return ans
}
```
- Runtime 0 ms, Memory 1.8 MB
```go
func countGoodSubstrings(s string) int {
	ans := 0

	for i := 0; i < len(s)-2; i++ {
		alpha := make([]byte, 26)
		alpha[s[i]-'a']++
		alpha[s[i+1]-'a']++
		alpha[s[i+2]-'a']++

		if alpha[s[i+1]-'a'] > 1 || alpha[s[i+2]-'a'] > 1 {
			continue
		}

		ans++
	}

	return ans
}
```


## 1971. Find if Path Exists in Graph

- https://leetcode.com/problems/find-if-path-exists-in-graph/
- `Depth-First Search` `Breadth-First Search` `Union Find` `Graph`
- Runtime 367 ms, Memoery 43.5 MB

```go
func validPath(n int, edges [][]int, start int, end int) bool {
	m := make(map[int][]int)
	for _, e := range edges {
		m[e[0]] = append(m[e[0]], e[1])
		m[e[1]] = append(m[e[1]], e[0])
	}

	visited := make(map[int]bool)
	stack := []int{start}

	for len(stack) != 0 {
		pop := stack[len(stack)-1]
		stack = stack[:len(stack)-1]

		if pop == end {
			return true
		}

		if visited[pop] {
			continue
		}

		visited[pop] = true
		stack = append(stack, m[pop]...)
	}

	return false
}
```


## 1290. Convert Binary Number in a Linked List to Integer

- https://leetcode.com/problems/convert-binary-number-in-a-linked-list-to-integer/
- `Linked List` `Math` `Linked List` `Math`
- Runtime 0 ms, Memory 2 MB
```go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func getDecimalValue(head *ListNode) int {
	ans := 0
	for head != nil {
		ans = ans * 2 + head.Val
		head = head.Next
	}
	return ans
}
```
- Runtime 0 ms, Memory 2 MB
```go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func getDecimalValue(head *ListNode) int {
	ans := 0
	for head != nil {
		ans = ans << 1 | head.Val
		head = head.Next
	}
	return ans
}
```


## 2363. Merge Similar Items

- https://leetcode.com/problems/merge-similar-items/
- `Array` `Hash Table` `Sorting` `Ordered Set`
- Runtime 18 ms, Memory 6.7 MB
```go
func mergeSimilarItems(items1 [][]int, items2 [][]int) [][]int {
	m := make(map[int]int, 1000)
	for _, v := range items1 {
		m[v[0]] += v[1]
	}
	for _, v := range items2 {
		m[v[0]] += v[1]
	}

	ans := make([][]int, 0, len(m))
	for v, w := range m {
		if w > 0 {
			ans = append(ans, []int{v, w})
		}
	}

	sort.Slice(ans, func(j, k int) bool {
		return ans[j][0] < ans[k][0]
	})

	return ans
}
```


## 1475. Final Prices With a Special Discount in a Shop

- https://leetcode.com/problems/final-prices-with-a-special-discount-in-a-shop/
- `Array` `Stack` `Monotonic Stack`
- Runtime 4 ms, Memory 3 MB
```go
func finalPrices(prices []int) []int {
	for i := 0; i < len(prices)-1; i++ {
		for j := i + 1; j < len(prices); j++ {
			if prices[j] <= prices[i] {
				prices[i] = prices[i] - prices[j]
				break
			}
		}
	}
	return prices
}
```


## 1534. Count Good Triplets

- https://leetcode.com/problems/count-good-triplets/
- `Array` `Enumeration`
- Runtime 7 ms, Memory 2.2 MB
```go
func countGoodTriplets(arr []int, a int, b int, c int) int {
	length := len(arr)
	if len(arr) < 3 {
		return 0
	}

	ans := 0
	for i := 0; i < length-2; i++ {
		for j := i + 1; j < length-1; j++ {
			if abs(arr[i]-arr[j]) > a {
				continue
			}
			for k := j + 1; k < length; k++ {
				if abs(arr[j]-arr[k]) > b {
					continue
				}
				if abs(arr[i]-arr[k]) > c {
					continue
				}
				ans++
			}
		}
	}

	return ans
}

func abs(n int) int {
	if n < 0 {
		return -n
	}
	return n
}
```


## 509. Fibonacci Number

- https://leetcode.com/problems/fibonacci-number/
- `Math` `Dynamic Programming` `Recursion` `Memoization`
- Runtime 15 ms, Memory 1.9 MB
```go
// Recursion
func fib(n int) int {
	if n < 2 {
		return n
	}
	return fib(n-1) + fib(n-2)
}
```
- Runtime 0 ms, Memory 2 MB
```go
// Memoization
func fib(n int) int {
	m := []int{0, 1, 1}
	for i := 3; i <= n; i++ {
		m = append(m, m[i-1]+m[i-2])
	}
	return m[n]
}
```
- Runtime 0 ms, Memory 1.9 MB
```go
func fib(n int) int {
	if n < 2 {
		return n
	}

	a, b := 0, 1
	for i := 1; i < n; i++ {
		a, b = b, a+b
	}
	return b
}
```


## 1763. Longest Nice Substring

- https://leetcode.com/problems/longest-nice-substring/
- `Hash Table` `String` `Divide and Conquer` `Bit Manipulation`
- Runtime 4 ms, Memory 2 MB
```go
func longestNiceSubstring(s string) string {
	ans := ""
	runes := []rune(s)

	for i := 0; i < len(runes); i++ {
		for j := len(runes); j > i+1; j-- {
			sub := runes[i:j]

			if isNice(sub) {
				if len(sub) > len(ans) {
					ans = string(sub)
				}
			}
		}
	}

	return ans
}

func isNice(runes []rune) bool {
	if len(runes) == 0 {
		return false
	}

	m := [52]bool{}
	for _, r := range runes {
		if r >= 'a' && r <= 'z' {
			m[r-'a'] = true
		} else {
			m[r-'A'+26] = true
		}
	}

	for i := 0; i < len(m); i++ {
		if !m[i] {
			continue
		}

		j := i

		if j < 26 {
			j += 26
		} else {
			j -= 26
		}

		if !m[j] {
			return false
		}
	}

	return true
}
```
- Runtime 0 ms, Memory 2.3 MB
```go
func longestNiceSubstring(s string) string {
	if len(s) < 2 {
		return ""
	}

	set := make(map[rune]bool)
	for _, r := range s {
		set[r] = true
	}

	for i, r := range s {
		if set[unicode.ToLower(r)] && set[unicode.ToUpper(r)] {
			continue
		}

		left := longestNiceSubstring(s[:i])
		right := longestNiceSubstring(s[i+1:])
		if len(left) >= len(right) {
			return left
		} else {
			return right
		}
	}

	return s
}
```


## 938. Range Sum of BST

- https://leetcode.com/problems/range-sum-of-bst/
- `Tree` `Depth-First Search` `Binary Search Tree` `Binary Tree`
- Runtime 103 ms, Memory 8.5 MB
```go
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func rangeSumBST(root *TreeNode, low int, high int) int {
	if root == nil {
		return 0
	}

	sum := 0
	if low <= root.Val && root.Val <= high {
		sum += root.Val
	}

	if root.Val > low {
		sum += rangeSumBST(root.Left, low, high)
	}

	if root.Val < high {
		sum += rangeSumBST(root.Right, low, high)
	}

	return sum
}
```
- Runtime 82 ms, Memory 9.1 MB
```go
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func rangeSumBST(root *TreeNode, low int, high int) int {
	if root == nil {
		return 0
	}

	sum := 0
	if low <= root.Val && root.Val <= high {
		sum += root.Val
	}

	sum +=  rangeSumBST(root.Left, low, high)
	sum +=  rangeSumBST(root.Right, low, high)

	return sum
}
```


## 933. Number of Recent Calls

- https://leetcode.com/problems/number-of-recent-calls/
- `Design` `Queue` `Data Stream`
- Runtime 124 ms, Memory 8.5 MB
```go
type RecentCounter struct {
	stack []int
}

func Constructor() RecentCounter {
	return RecentCounter{}
}

func (rc *RecentCounter) Ping(t int) int {
	rc.stack = append(rc.stack, t)
	min := t - 3000

	for i, v := range rc.stack {
		if v >= min {
			rc.stack = rc.stack[i:]
			return len(rc.stack)
		}
	}

	return 0
}

/**
 * Your RecentCounter object will be instantiated and called as such:
 * obj := Constructor();
 * param_1 := obj.Ping(t);
 */
 ```
