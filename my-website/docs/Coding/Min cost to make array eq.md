2448. Minimum Cost to Make Array Equal

You are given two 0-indexed arrays nums and cost consisting each of n positive integers.

You can do the following operation any number of times:

    Increase or decrease any element of the array nums by 1.

The cost of doing one operation on the ith element is cost[i].

Return the minimum total cost such that all the elements of the array nums become equal.

crazy math proof
https://leetcode.com/problems/minimum-cost-to-make-array-equal/solutions/2734728/Pure-math-based-explanation-of-why-Cost-Function-is-convex/

Explanation

Assume the final equal values are x
the total cost function y = f(x) is a convex function
on the range of [min(A), max(A)].

To find the minimum value of f(x),
we can binary search x by comparing f(mid) and f(mid + 1).

If f(mid) <= f(mid + 1),
the minimum f(x) is on the left of mid,
where x <= mid

If f(mid) >= f(mid + 1),
the minimum f(x) is on the right of mid + 1,
where x >= mid.

Repeatly doing this while left < right,
until we find the minimum value and return it.

This method is known as trinary search,
if we check f(mid1) and f(mid2).

```
func minCost(nums []int, cost []int) int64 {
    arr := [][2]int{}
    for i, num := range nums {
        arr = append(arr, [2]int{num, cost[i]})
    }
    
    l, r := 0, 0
    for _, num := range nums {
        l = min(l, num)
        r = max(r, num)
    }
    
    for l < r {
        mid := l + (r-l)/2
        cost1, cost2 := getCost(arr, mid), getCost(arr, mid+1)
        if cost1 < cost2 { // minimum exists in left side
            r = mid
        } else { // minimum exists in right side
            l = mid+1
        }
    }
    
    return getCost(arr, l)
}

func getCost(numWtCost [][2]int, target int) int64 {
    var total int64
    for _, item := range numWtCost {
        num, cost := item[0], item[1]
        total += int64(abs((num-target))*cost)
    }
    
    return total
}

func abs(num int) int {
    if num < 0 {
        return -num
    }
    
    return num
}

func min(a, b int) int {
    if a < b {
        return a
    }
    
    return b
}

func max(a, b int) int {
    if a > b {
        return a
    }
    
    return b
}
```

Can be done either DP or mathematical way of ternayr search

Explanation from Votrubac about DP
I'd say DP is the "go to" solution for the interview.

Binary search needs some reasoning, and the weighted median is quite tricky.
DP

In the end, all elements of the array will be equal to some element n[i].

    Well, you say, if our array is [2, 5], what if we can achieve min cost by making them 3 or 4?
    For this to be the case, the cost for both 2 and 5 must be the same. But if the cost the same, we can achieve the same min cost if we pick 2 or 5.

Let's call it a pivot.

If we sort the array, elements on the left of the pivot will increase, and on the right - decrease.

We go left-to-right in the sorted array, and compute cost for each pivot (cost_l[i]).

Then we do the same right-to-left, compute cost (cost_r), track and the minimum total cost (min(cost_l[i], cost_r)).

DP Way:
```
long long minCost(vector<int>& n, vector<int>& cost) {
    vector<long long> id(n.size()), cost_l(n.size());
    iota(begin(id), end(id), 0);
    sort(begin(id), end(id), [&](int i, int j){
        return n[i] < n[j];
    });
    for (long long i = 0, psum = 0; i < n.size() - 1; ++i) {
        psum += cost[id[i]];
        cost_l[i + 1] = cost_l[i] + psum * (n[id[i + 1]] - n[id[i]]);
    }
    long long res = cost_l.back(), cost_r = 0;
    for (long long j = n.size() - 1, psum = 0; j > 0; --j) {
        psum += cost[id[j]];
        cost_r += psum * (n[id[j]] - n[id[j - 1]]);
        res = min(res, cost_l[j - 1] + cost_r);
    }
    return res;
}
```


