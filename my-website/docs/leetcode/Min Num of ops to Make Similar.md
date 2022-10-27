2449. Minimum Number of Operations to Make Arrays Similar

You are given two positive integer arrays nums and target, of the same length.

In one operation, you can choose any two distinct indices i and j where 0 <= i, j < nums.length and:

    set nums[i] = nums[i] + 2 and
    set nums[j] = nums[j] - 2.

Two arrays are considered to be similar if the frequency of each element is the same.

Return the minimum number of operations required to make nums similar to target. The test cases are generated such that nums can always be similar to target.

Explanation:
We need to match odd numbers in n with odd numbers in target, and even with even.

We sort both arrays first. We use two pointers to indicate the smallest odd and even element in target.

We pick the next smallest number from n, and match with the next smallest (odd or even) in target.

The cost is res += abs(n[i] - t[j]) / 2. Note that this results in double-counting, so we return res / 2 in the end.

```
func makeSimilar(nums []int, target []int) int64 {
    sort.Ints(nums)
    sort.Ints(target)
    
    numOdd, numEvn := []int{}, []int{}
    tgtOdd, tgtEvn := []int{}, []int{}
    
    for i, num := range nums {
        if num&1 == 0 {
            numEvn = append(numEvn, num)
        } else {
            numOdd = append(numOdd, num)
        }
        
        if target[i]&1 == 0 {
            tgtEvn = append(tgtEvn, target[i])
        } else {
            tgtOdd = append(tgtOdd, target[i])
        }
    }
    
    ops := 0
    for i, num := range numEvn {
        ops += abs(num-tgtEvn[i])/2
    }
    for i, num := range numOdd {
        ops += abs(num-tgtOdd[i])/2
    }
    return int64(ops/2)
}

func abs(num int) int {
    if num < 0 {
        return -num
    }
    
    return num
}
```