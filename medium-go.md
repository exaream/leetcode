# Medium Level Problems

- https://leetcode.com/problemset/all/?page=1&sorting=W3sic29ydE9yZGVyIjoiREVTQ0VORElORyIsIm9yZGVyQnkiOiJGUk9OVEVORF9JRCJ9XQ%3D%3D&status=NOT_STARTED&listId=wpwgkgt&difficulty=MEDIUM

## 454. 4Sum II

- https://leetcode.com/problems/4sum-ii/
- `Array` `Hash Table`
- Runtime 70 ms, Memory 8.3 MB

```go
func fourSumCount(nums1, nums2, nums3, nums4 []int) int {
	ans := 0
	tmp := make(map[int]int, len(nums1)*len(nums2))

	for _, i := range nums1 {
		for _, j := range nums2 {
			tmp[i+j]++
		}
	}

	for _, k := range nums3 {
		for _, l := range nums4 {
			ans += tmp[-(k + l)] // Add the zero value 0 to ans if tmp[-(k + l)] does NOT exist
		}
	}

	return ans
}
```


## 395. Longest Substring with At Least K Repeating Characters

- https://leetcode.com/problems/longest-substring-with-at-least-k-repeating-characters/
- `Hash Table` `String` `Divide and Conquer` `Sliding Window`
- Runtime 0 ms, Memory 2.2 MB

```go
func longestSubstring(s string, k int) int {
	if len(s) < k {
		return 0
	}

	if k == 1 {
		return len(s)
	}

	cnt := make([]int, 26)
	for _, c := range s {
		cnt[c-'a']++
	}

	badChar := ""
	for i, v := range cnt {
		if v > 0 && v < k {
			badChar = string(i + 'a')
			break
		}
	}

	if badChar == "" {
		return len(s)
	}

	parts := strings.Split(s, badChar)
	ans := 0
	for _, v := range parts {
		ans = max(ans, longestSubstring(v, k))
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


## 384. Shuffle an Array

- https://leetcode.com/problems/shuffle-an-array/
- `Array` `Math` `Randomized`
- Runtime 24 ms, Memory 8 MB
```go
type Solution struct {
	org []int
	tmp []int
}

func Constructor(nums []int) Solution {
	rand.Seed(time.Now().UnixNano())
	return Solution{
		org: nums,
		tmp: make([]int, len(nums)),
	}
}

func (s *Solution) Reset() []int {
	return s.org
}

func (s *Solution) Shuffle() []int {
	copy(s.tmp, s.org)
	rand.Shuffle(len(s.tmp), func(i, j int) { s.tmp[i], s.tmp[j] = s.tmp[j], s.tmp[i] })
	return s.tmp
}
```


## 237. Delete Node in a Linked List

- https://leetcode.com/problems/delete-node-in-a-linked-list/
- `Linked List`
- Runtime 4 ms, Memory 2.8 MB

```go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func deleteNode(node *ListNode) {
	*node = *node.Next
}
```

- Runtime 0 ms, Memory 2.8 MB
```go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func deleteNode(node *ListNode) {
	node.Val = node.Next.Val
	node.Next = node.Next.Next
}
```


## 46. Permutations

- https://leetcode.com/problems/permutations/
- `Array` `Backtracking`
- Runtime 0 ms, Memory 2.5 MB
```go
func permute(nums []int) [][]int {
	ans := make([][]int, 0)
	dfs(&ans, nums, 0)
	return ans
}

// Depth First Search
func dfs(ans *[][]int, nums []int, start int) {
	if start >= len(nums) {
		tmp := make([]int, len(nums)) //be careful of these two lines
		copy(tmp, nums)
		*ans = append(*ans, tmp)
		return
	}
	for i := start; i < len(nums); i++ {
		nums[start], nums[i] = nums[i], nums[start]
		dfs(ans, nums, start+1)
		nums[start], nums[i] = nums[i], nums[start]
	}
}
```


## 142. Linked List Cycle II

- https://leetcode.com/problems/linked-list-cycle-ii/
- `Hash Table` `Linked List` `Two Pointers`
- Runtime 6 ms, Memory 5 MB
```go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func detectCycle(head *ListNode) *ListNode {
	if head == nil {
		return nil
	}

	m := make(map[*ListNode]bool)
	for head != nil {
		if m[head] {
			return head
		}
		m[head] = true
		head = head.Next
	}
	
	return nil
}
```
- Runtime 3 ms, Memory 3.6 MB
```go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func detectCycle(head *ListNode) *ListNode {
	if head == nil {
		return nil
	}

	slow, fast := head, head

	for fast.Next != nil && fast.Next.Next != nil {
		slow, fast = slow.Next, fast.Next.Next
		if fast != slow {
			continue
		}

		for head != slow {
			slow, head = slow.Next, head.Next
		}

		return head
	}

	return nil
}
```
- Runtime 3 ms, Memory 3.6 MB
```go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func detectCycle(head *ListNode) *ListNode {
	if head == nil {
		return nil
	}

	slow, fast := head, head
	var isCycle bool

	for fast != nil && fast.Next != nil {
		slow, fast = slow.Next, fast.Next.Next
		if slow == fast {
			isCycle = true
			break
		}
	}

	if !isCycle {
		return nil
	}

	for head != slow {
		slow, head = slow.Next, head.Next
	}

	return head
}
```
