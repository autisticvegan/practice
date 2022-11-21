Median of 2 Sorted Arrays

```
Given two sorted arrays nums1 and nums2 of size m and n respectively, return the median of the two sorted arrays.

The overall run time complexity should be O(log (m+n)).
```

```
func findMedianSortedArrays(nums1 []int, nums2 []int) float64 {
	a, b := nums1, nums2
	m, n := len(a), len(b)
	if m > n {
		a, b, m, n = b, a, n, m
	}
	imin, imax := 0, m
	var i, j int
	for imin <= imax {
		i = (imin + imax) / 2
		j = (m+n+1)/2 - i
		switch {
		case i < m && b[j-1] > a[i]:
			imin = i + 1
		case i > 0 && a[i-1] > b[j]:
			imax = i - 1
		default:
			var leftMax float64
			if i == 0 {
				leftMax = float64(b[j-1])
			} else if j == 0 {
				leftMax = float64(a[i-1])
			} else {
				leftMax = math.Max(float64(a[i-1]), float64(b[j-1]))
			}

			if (m+n)%2 == 1 {
				return leftMax
			}

			var rightMin float64
			if i == m {
				rightMin = float64(b[j])
			} else if j == n {
				rightMin = float64(a[i])
			} else {
				rightMin = math.Min(float64(a[i]), float64(b[j]))
			}
			return (leftMax + rightMin) / 2
		}
	}
	return 0
}
```