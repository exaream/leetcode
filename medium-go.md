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
			ans += tmp[-(k + l)] // ans += 0  if  tmp[-(k + l)]  does NOT exist
		}
	}

	return ans
}
```
