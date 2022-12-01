# Easy Level
- https://leetcode.com/problemset/all/?page=1&difficulty=EASY


## 2235. Add Two Integers

```go
func sum(num1 int, num2 int) int {
	return num1 + num2
}
```


## 1480. Running Sum of 1D Array

```go
func runningSum(nums []int) []int {
	numsLen := len(nums)
	res := make([]int, numsLen)
	res[0] = nums[0]

	for i := 1; i < numsLen; i++ {
		res[i] = nums[i] + res[i-1]
	}

	return res
}
```


## 1672. Richest Customer Wealth

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

```go
func fizzBuzz(n int) []string {
	res := make([]string, n)

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

		res[i-1] = str
	}

	return res
}
```


## 1342. Number of Steps to Reduce a Number to Zero

```go
func numberOfSteps(num int) int {
	if num <= 0 {
		return 0
	}

	res := 0
	for num > 0 {
		if num%2 == 0 {
			num /= 2
		} else {
			num--
		}

		res++
	}

	return res
}
```

```go
func numberOfSteps(num int) int {
	if num == 0 {
		return 0
	}

	res := 0
	for num > 0 {
		res += num&1 + 1
		num >>= 1
	}

	return res - 1
}
```


## 876. Middle of The Linked List

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
```go
func twoSum(nums []int, target int) []int {
	m := make(map[int]int)

	for idx, num := range nums {
		if preIdx, ok := m[target-num]; ok {
			return []int{preIdx, idx}
		}
		m[num] = idx
	}

	return nil
}
```
