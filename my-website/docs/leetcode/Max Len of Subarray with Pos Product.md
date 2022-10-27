1567. Maximum Length of Subarray With Positive Product

Given an array of integers nums, find the maximum length of a subarray where the product of all its elements is positive.

A subarray of an array is a consecutive sequence of zero or more values taken out of that array.

Return the maximum length of a subarray with positive product.

```
func max(x, y int) int {
    if x > y {
        return x
    }
    return y
}

func getMaxLen(nums []int) int {
    res := 0
    // 2 lengths, pos and neg
    // pos is max len of subarr with pos product
    // neg is max len of subarr with neg product (i.e. neg nums % 2 == 1)
    // we update max every iter, with pos len, because pos len is also updated with neglen in the neg case
    currPosLen := 0
    currNegLen := 0

    // if we see a 0, reset the curr lens to 0
    // else if its pos, then  incr pos len. if nelen is not 0, then also incr it
    // else if its neg, then do a bunch of things 
    for i := 0; i < len(nums); i++ {

        if nums[i] == 0 {
            currNegLen = 0
            currPosLen = 0
        } else if nums[i] > 0 {
            currPosLen++
            if currNegLen != 0 {
                currNegLen++
            }
        } else {
            prevPos := currPosLen
            if currNegLen == 0 {
                currPosLen = 0
            } else {
                currPosLen = currNegLen + 1
            }
            currNegLen = prevPos + 1
        }
        res = max(res, currPosLen)
    }
    return res
}

```