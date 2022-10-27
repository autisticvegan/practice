2448. Minimum Cost to Make Array Equal

You are given two 0-indexed arrays nums and cost consisting each of n positive integers.

You can do the following operation any number of times:

    Increase or decrease any element of the array nums by 1.

The cost of doing one operation on the ith element is cost[i].

Return the minimum total cost such that all the elements of the array nums become equal.

Example 1:
```
Input: nums = [1,3,5,2], cost = [2,3,1,14]
Output: 8
Explanation: We can make all the elements equal to 2 in the following way:
- Increase the 0th element one time. The cost is 2.
- Decrease the 1st element one time. The cost is 3.
- Decrease the 2nd element three times. The cost is 1 + 1 + 1 = 3.
The total cost is 2 + 3 + 3 = 8.
It can be shown that we cannot make the array equal with a smaller cost.
```
Example 2:
```
Input: nums = [2,2,2,2,2], cost = [4,2,8,1,3]
Output: 0
Explanation: All the elements are already equal, so no operations are needed.
```

Can be done either DP or mathematical way of ternayr search

Search:
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






