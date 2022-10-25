
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



Explanation from Votrubac:
Count GCDs O(n log m)

For an element num[i], we count GCDs produced by subarrays:

    nums[i - 1]
    nums[i - 2], nums[i - 1]
    nums[i - 3], nums[i - 2], nums[i - 1]
    ...and so on.

The number of distinct GCDs would not exceed log(m), where m is the maximum value in the array.

    Note that those disticnt GCDs should share a factor k, and come from subarrays ending at some position.
    To produce a different GCD, gcd(n[i], gcd(n[i - 2], n[i - 1]) should be bigger than gcd(n[i - 2], n[i - 1]).
    Therefore n[i - 1] < n[i], and n[i - 1] * f == n[i].
    The best we can do is something like [2, 4, 8, 16, 32, ...], and the number of unique GCDs will therefore be log m.
