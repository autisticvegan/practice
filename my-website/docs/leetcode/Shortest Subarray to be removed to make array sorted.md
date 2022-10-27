


C++
```
    int sz = n.size(), r = sz - 1;
    for (; r > 0 && n[r - 1] <= n[r]; --r) ;
    auto res = r;
    for (int l = 0; l < r && (l == 0 || n[l - 1] <= n[l]); ++l) {
        while (r < sz && n[r] < n[l])
            ++r;
        res = min(res, r - l - 1);
    }
    return res;

```

Go
```
// step 1, find the furthest right point where we have a mountain (i.e. n[r-1] > n[r])
// step 2, iter from left side while increasing, 
//         updating res each time, and while n[r] < n[l] r++ 

func min(x, y int) int {
    if x < y {
        return x
    }
    return y
}

func findLengthOfShortestSubarray(arr []int) int {
    farthestRight := len(arr) - 1

    for ; farthestRight > 0 && arr[farthestRight - 1] <= arr[farthestRight]; farthestRight-- {
    }

    res := farthestRight

    for left := 0; (left < farthestRight && (left == 0 || arr[left-1] <= arr[left])); left++ {

        for ; farthestRight < len(arr) && arr[farthestRight] < arr[left]; farthestRight++ {
        }
        
        res = min(res, farthestRight - left - 1)

    }

    return res
}

```

Follow up: what if it is allowed to be more than one subarray, rather than just one?
Answer: It becomes longest increasing or non-decreasing subsequence problem, which is n^2 using DP
