
Given an unsorted integer array nums, return the smallest missing positive integer.

You must implement an algorithm that runs in O(n) time and uses constant extra space.

idea is to use the space in the array and swapping to keep track of thingns - goes from 1 to nlen + 1
```
func firstMissingPositive(nums []int) int {
	nlen := len(nums)
	for i := 0; i < nlen; i++ {
		if nums[i] >= 1 && nums[i] <= nlen && nums[i] != nums[nums[i]-1] {
			nums[i], nums[nums[i]-1] = nums[nums[i]-1], nums[i]
			i-- // keep the same index
		}
	}

	for i := 0; i < nlen; i++ {
		if nums[i] != i+1 {
			return i + 1
		}
	}
	return nlen + 1
}
```