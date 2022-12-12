# Easy Level Problems

- https://leetcode.com/problemset/all/?page=1&difficulty=EASY
- https://leetcode.com/explore/interview/card/top-interview-questions-easy/

## 2235. Add Two Integers

- https://leetcode.com/problems/add-two-integers/
- `Math`
- Runetime 2 ms, Memory 1.9 MB
```go
func sum(num1 int, num2 int) int {
	return num1 + num2
}
```


## 1480. Running Sum of 1d Array

- https://leetcode.com/problems/running-sum-of-1d-array/
- `Array`, `Prefix Sum`
- Runetime 8 ms, Memory 2.8 MB
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
- `Array`, `Matrix`
- Runetime 7 ms, Memory 3.1 MB
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
- `Math`, `String`, `Simulation`
- Runetime 11 ms, Memory 3.6 MB
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
- `Math`, `Bit Manipulation`
- Runetime 4 ms, Memory 1.9 MB
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

- Runetime 0 ms, Memory 1.8 MB
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
- `Linked List`, `Two Pointers`
- Runetime 0 ms, Memoery 2.1 MB
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

- Runetime 3 ms, Memoery 2 MB
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
- `Hash Table`, `String`, `Counting`
- Runetime 7 ms, Memory 3.8 MB
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
- `Array`, `Hash Table`
- brute force
- Runetime 33 ms, Memory 3.5 MB
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
- Runetime 0 ms, Memory 4.3 MB
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
- `String`, `Counting`
- Runetime 0ms, Memory 2.2MB
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
- `Hash Table`, `Math`, `String`
- Runetime 19 ms, Memory 2.9 MB
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

- Runetime 8 ms, Memory 2.9 MB
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
- Runetime 0 ms, Memory 2.4 MB
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
- `String`, `Stack`
- Runetime 0 ms, Memory 2 MB
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
- `Linked List`, `Recursion`
- Runetime 0 ms, Memory 2.5 MB
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
- `Array`, `Two Pointers`
- Runetime 7 ms, Memory 4.3 MB
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
- `Array`, `Dynamic Programming`
- Runetime 179 ms, Memory 9 MB
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

- Runetime 158 ms, Memory 9.4 MB
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
- `Array`, `Math`
- Runetime 0 ms, Memory 2.1 MB
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
- `Array`, `Two Pointers`
- Runetime 26 ms, Memory 6.6 MB
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
- `Array`, `Hash Table`, `Sorting`
- Runetime 155 ms, Memory 8.5 MB
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

- Runetime 70 ms, Memory 8.6 MB
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
- `Array`, `Bit Manipulation`
- Runetime 18 ms, Memory 6.7 MB
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
- Runetime 13 ms, Memory 6.2 MB
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
- `Array`, `Hash Table`, `Two Pointers`, `Binary Search`, `Sorting`
- Runetime 5 ms, Memory 2.8 MB
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

- Runetime 4 ms, Memory 3 MB
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
- `Array`, `Hash Table`, `Two Pointers`, `Binary Search`, `Sorting`
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
- `Two Pointers`, `String`
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
- `Hash Table`, `String`, `Sorting`
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
- `Two Pointers`, `String`
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
- `Linked List`, `Recursion`
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
-  `Tree`,  `Depth-First Search`,  `Breadth-First Search`, `Binary Tree`
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
- `Array`, `Divide and Conquer`, `Tree`, `Binary Search Tree`, `Binary Tree`
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
- `Array`, `Two Pointers`, `Sorting`
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
- `Binary Search`, `Interactive`
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
- `Dynamic Programming`, `Memoization`
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
- `Math`, `Recursion`
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
- `Divide and Conquer`, `Bit Manipulation`
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
- `Divide and Conquer`, `Bit Manipulation`
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
