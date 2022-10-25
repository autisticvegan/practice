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

Note you can also do the backtracking way, which works for both with duplicates and without duplicates (Subsets II)

Subsets I
```
class Solution {
public:
    std::vector<std::vector<int> > subsets(std::vector<int> &nums) {
		std::sort(nums.begin(), nums.end());
        std::vector<std::vector<int> > res;
		std::vector<int> vec;
		subsets(res, nums, vec, 0);
		return res;
    }
private:
	void subsets(std::vector<std::vector<int> > &res, std::vector<int> &nums, std::vector<int> &vec, int begin) {
		res.push_back(vec);
		for (int i = begin; i != nums.size(); ++i) {
			vec.push_back(nums[i]);
			subsets(res, nums, vec, i + 1);
			vec.pop_back();
		}
	}
};
```

Subsets II
```
class Solution {
public:
    std::vector<std::vector<int> > subsetsWithDup(std::vector<int> &nums) {
		std::sort(nums.begin(), nums.end());
        std::vector<std::vector<int> > res;
		std::vector<int> vec;
		subsetsWithDup(res, nums, vec, 0);
		return res;
    }
private:
	void subsetsWithDup(std::vector<std::vector<int> > &res, std::vector<int> &nums, std::vector<int> &vec, int begin) {
		res.push_back(vec);
		for (int i = begin; i != nums.size(); ++i)
			if (i == begin || nums[i] != nums[i - 1]) { 
				vec.push_back(nums[i]);
				subsetsWithDup(res, nums, vec, i + 1);
				vec.pop_back();
			}
	}
};
```

Go
```
func subsets(nums []int) [][]int {
    res := make([][]int, 0)
    solve(nums, nil, &res)
    return res
}

func solve(nums []int, cur []int, res *[][]int) { 
    *res = append(*res, append([]int{}, cur...)) 
    for i := 0; i < len(nums); i++ {
        solve(nums[i+1:], append(cur, nums[i]), res)
    }
}
```

Subsets II

```
func subsetsWithDup(nums []int) [][]int {
	res := [][]int{[]int{}}
	var cur []int

	sort.Ints(nums)
	doSubsetsWithDup(nums, cur, &res)
	return res
}

func doSubsetsWithDup(nums []int, cur []int, res *[][]int) {
	for i := 0; i < len(nums); i++ {
		if i > 0 && nums[i] == nums[i-1] {
			continue
		}
		cur = append(cur, nums[i])
		newRes := make([]int, len(cur))
		copy(newRes, cur)
		*res = append(*res, newRes)

		doSubsetsWithDup(nums[i+1:], cur, res)
		cur = cur[:len(cur)-1]
	}
}
```