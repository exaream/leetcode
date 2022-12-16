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

	splited := strings.Split(s, badChar)
	ans := 0
	for _, v := range splited {
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
