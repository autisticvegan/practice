




- Similar to Best Time to Buy and Sell Stock III, but instead of maximum profit, we track maximum sum of N elements.

- Left-to-right, track the maximum sum of L elements in left. Right-to-left, track the maximum sum of M elements in right.

- Then, find the split point where left[i] + right[i] gives us the maximum sum.

- we need to do it twice for (L, M) and (M, L).

```
func max(x, y int) int {
    if x > y {
        return x
    }
    return y
}

func maxTwoNoOverlap(nums []int, leftSize, rightSize int) int {
    res := 0
    leftMemo := make([]int, len(nums) + 1)
    rightMemo := make([]int, len(nums) + 1)
    sumRight := 0
    sumLeft := 0
    for i,j := 0, len(nums)-1; i < len(nums); i, j = i + 1, j - 1 {
        sumLeft += nums[i]
        sumRight += nums[j]

        leftMemo[i + 1] = max(sumLeft, leftMemo[i])
        rightMemo[j] = max(sumRight, rightMemo[j + 1])

        // if we are going outside the window, we need to subtract off the start
        if i + 1 >= leftSize {
            sumLeft -= nums[i-leftSize + 1]
        }
        if i + 1 >= rightSize {
            sumRight -= nums[j + rightSize - 1]
        }

    }

    for i := 0; i < len(nums); i++ {
        res = max(res, leftMemo[i] + rightMemo[i])
    }

    return res
}


func maxSumTwoNoOverlap(nums []int, firstLen int, secondLen int) int {
    return max(maxTwoNoOverlap(nums, firstLen, secondLen), maxTwoNoOverlap(nums, secondLen, firstLen))
}
```