
half recursion,
```
func search(nums []int, target int) int {
    n := len(nums)
    
    // Find the pivot.
    left, right := 0, n-1
    for left < right {
        mid := left+(right-left)/2
        if nums[mid] > nums[right] {
            left = mid+1
        } else {
            right = mid
        }
    }
    
    pivot := left
    
	// Regular binary search
    left, right = pivot, pivot-1+n
    for left <= right {
        mid := left+(right-left)/2
        midVal := nums[mid % n]
        
        if midVal > target {
            right = mid-1
        } else if midVal < target {
            left = mid+1
        } else {
            return mid % n
        }
    }
    
    return -1
}
```

---
tags: [half-check, Binary-Search]
---