
Get the go GCD func from x

The idea here is that we memoize for previously found GCDs, leading to nlogn instead of n^2

```
func subarrayGCD(nums []int, k int) int {
    res := 0
    gcds := make(map[int]int)
    for i := 0; i < len(nums); i++ {
        newGcds := make(map[int]int)
        if nums[i] % k == 0 {
            gcds[nums[i]]++
            for k, v := range gcds {
                newGcds[gcd(k, nums[i])] += v
            }
        }
        res += newGcds[k]
        gcds = newGcds
    }
    return res
}
```