lc 2340

`
You are given a 0-indexed integer array nums.

Swaps of adjacent elements are able to be performed on nums.

A valid array meets the following conditions:

    The largest element (any of the largest elements if there are multiple) is at the rightmost position in the array.
    The smallest element (any of the smallest elements if there are multiple) is at the leftmost position in the array.

Return the minimum swaps required to make nums a valid array.
`


`func minimumSwaps(nums []int) int {
	minNum, maxNum := math.MaxInt, math.MinInt
    minIdx, maxIdx := 0, 0
	// get min/max values and their indexes in O(N)
	for i, n := range nums {
        if n < minNum {
			minIdx = i
			minNum = n
		}
        if n >= maxNum {
			maxIdx = i
			maxNum = n
		}
	}
 
    // quick mafs
    swaps := minIdx + (len(nums)-maxIdx-1)
	
	// if minNum index is > maxNum index that means they'll pass eachother one time during swapping
	// we can subtract 1 here to adjust the math
    if minIdx > maxIdx {
        swaps--
    }

    return swaps
}
`