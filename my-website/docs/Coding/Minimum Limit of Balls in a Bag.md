Minimum Limit of Balls in a Bag  

```
ou are given an integer array nums where the ith bag contains nums[i] balls. You are also given an integer maxOperations.

You can perform the following operation at most maxOperations times:

    Take any bag of balls and divide it into two new bags with a positive number of balls.
        For example, a bag of 5 balls can become two new bags of 1 and 4 balls, or two new bags of 2 and 3 balls.

Your penalty is the maximum number of balls in a bag. You want to minimize your penalty after the operations.

Return the minimum possible penalty after performing the operations.
```

```
func max(x, y int) int {
    if x > y {
        return x
    }
    return y
}


func getMax(nums []int) int {
    maxVal := -99999

    for _, x := range nums {
        maxVal = max(maxVal, x)
    }

    return maxVal
}

func calcPenalty(nums []int, mid, maxOps int) bool {
    count := 0
    for _, x := range nums {
        count += (x - 1) / mid
    }

    return count <= maxOps
}

// binary search
// think about split formula of num - 1 / mid
func minimumSize(nums []int, maxOperations int) int {
    
    left := 1
    right := getMax(nums)

    for left < right {
        mid := left + (right - left) / 2

        if calcPenalty(nums, mid, maxOperations) {
            right = mid
        } else {
            left = mid + 1
        }
    }

    return left

}
```