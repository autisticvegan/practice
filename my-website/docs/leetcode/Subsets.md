Subsets

Given an integer array nums of unique elements, return all possible subsets (the power set).

The solution set must not contain duplicate subsets. Return the solution in any order.

Example 1:
```
Input: nums = [1,2,3]
Output: [[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]
```
Example 2:
```
Input: nums = [0]
Output: [[],[0]]
```


```
    std::vector<std::vector<int>> subsets(std::vector<int>& nums) {
        
        //idea-no sorting necessary, just initialize size
        //then use bitshifting: i >> j & 1 .  we are going vertical
        //res[i].push_back(j)
        //0 to p, 0 to n where p is 2^n
     
        long long iters = std::pow(2, nums.size());
        std::vector<std::vector<int>> res(iters);
        for(int i = 0; i < iters; ++i) {
            for(int j = 0; j < nums.size(); ++j) {
                if((i >> j) & 1) {
                    res[i].push_back(nums[j]);
                }
            }
        }
        
        return res;
    }
```