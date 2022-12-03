# Easy Level Problems
- https://leetcode.com/problemset/all/?page=1&difficulty=EASY
- https://leetcode.com/explore/interview/card/top-interview-questions-easy/

## 2235. Add Two Integers

Runtime 2 ms, Memory 1.9 MB
```go
func sum(num1 int, num2 int) int {
	return num1 + num2
}
```


## 1480. Running Sum of 1D Array

Runtime 8 ms, Memory 2.8 MB
```go
func runningSum(nums []int) []int {
	numsLen := len(nums)
	ans := make([]int, numsLen)
	ans[0] = nums[0]

	for i := 1; i < numsLen; i++ {
		ans[i] = nums[i] + ans[i-1]
	}

	return ans
}
```


## 1672. Richest Customer Wealth

Runtime 7 ms, Memory 3.1 MB
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

Runtime 11 ms, Memory 3.6 MB
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

Runtime 4 ms, Memory 1.9 MB
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

Runtime 3 ms, Memoery 2 MB
```go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func middleNode(head *ListNode) *ListNode {
	tmp := make([]*ListNode, 0)

	for head != nil {
		tmp = append(tmp, head)
		head = head.Next
	}

	return tmp[len(tmp)/2]
}
```

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

Runtime 7 ms, Memory 3.8 MB
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

brute force
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

hashmap
Runtime 0 ms, Memory 4.3 MB
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

Runtime 0ms, Memory 2.2MB
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

Runtime 19 ms, Memory 2.9 MB
```go
func romanToInt(s string) int {
	list := map[byte]int{'I': 1, 'V': 5, 'X': 10, 'L': 50, 'C': 100, 'D': 500, 'M': 1000}
	length := len(s)
	total := 0

	for i := 0; i < length; {
		if (i+1 < length) && (list[s[i]] < list[s[i+1]]) {
			total += list[s[i+1]] - list[s[i]]
			i += 2
		} else {
			total += list[s[i]]
			i += 1
		}
	}

	return total
}
```

Runtime 8 ms, Memory 2.9 MB
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

Runtime 0 ms, Memory 2.4 MB
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

Runtime 0 ms, Memory 2 MB
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

Runtime 0 ms, Memory 2.5 MB
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

Runtime 7 ms, Memory 4.3 MB
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

Runtime 179 ms, Memory 9 MB
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

Runtime 158 ms, Memory 9.4 MB
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
