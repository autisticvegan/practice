```
You are given an integer array nums and an array queries where queries[i] = [vali, indexi].

For each query i, first, apply nums[indexi] = nums[indexi] + vali, then print the sum of the even values of nums.

Return an integer array answer where answer[i] is the answer to the ith query.
```

```
0/5

func sumEvenAfterQueries(nums []int, queries [][]int) []int {
    
    sum := 0
    res := []int{}
    
    for _, x := range nums {
        if x % 2 == 0 {
            sum += x
        }
    }

    for _, q := range queries {

        initialVal := nums[q[1]]
        addThis := q[0]
        // case 2
        nums[q[1]] += addThis
        
        // case 1 and 4
        if nums[q[1]] % 2 == 0 {
            sum += nums[q[1]]
        }

        // case 1 and 3
        if initialVal % 2 == 0 {
            sum -= initialVal
        }

        res = append(res, sum)
    }

    //orig, query
    // even + even = minus the original even, add the new even (as in, add the difference)
    // odd + even = do nothing except update
    // even + odd = subtract the original even
    // odd + odd = add the new sum (its an even) 


    return res
}
```