945. Minimum Increment to Make Array Unique

You are given an integer array nums. In one move, you can pick an index i where 0 <= i < nums.length and increment nums[i] by 1.

Return the minimum number of moves to make every value in nums unique.

```
func minIncrementForUnique(A []int) int {
    num2Count := []int{}
    for _, a := range A {
        for len(num2Count) <= a {
            num2Count = append(num2Count, 0)
        }
        num2Count[a]++
    }
    // 0 -> 0
    // 1 -> 2 + 1
    // 2 -> 3 + 2
    // 3 -> 3 + 2
    // 4 -> 2 + 1
    // ...
    // 7 -> 1
    cost := 0
    idx := 0
    for {
        if idx >= len(num2Count) {
            break
        }
        val := num2Count[idx]
        if val > 1 {
            cost += val - 1
            if idx+1 >= len(num2Count) {
                num2Count = append(num2Count, 0)
            }
            num2Count[idx+1] += val - 1
        }
        idx++
    }
    return cost
}
```