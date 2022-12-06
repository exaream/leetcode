# Easy Level Problems

- https://leetcode.com/problemset/all/?page=1&difficulty=EASY
- https://leetcode.com/explore/interview/card/top-interview-questions-easy/

## 2235. Add Two Integers

- https://leetcode.com/problems/add-two-integers/
- Runetime 2 ms, Memory 1.9 MB
```go
func sum(num1 int, num2 int) int {
	return num1 + num2
}
```


## 1480. Running Sum of 1d Array

- https://leetcode.com/problems/running-sum-of-1d-array/
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