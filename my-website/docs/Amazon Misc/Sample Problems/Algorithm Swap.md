The following algorithm is used to sort an array of distinct n integers:
For the input array arr of size n do:
- Try to find the smallest pair of indices 0 ≤ i < j ≤ n-1 such that arr[i] > arr[j]. Here smallest means usual 
alphabetical ordering of pairs, i.e. (i1, j1) < (i2, j2) if and only if i1 < i2 or (i1 = i2 and j1 < j2).
- If there is no such pair, stop.
- Otherwise, swap a[i] and a[j] and repeat finding the next pair.


The algorithm seems to be correct, but the question is how efficient is it? Write a function that returns the 
number of swaps performed by the above algorithm.
For example, if the initial array is [5,1,4,2], then the algorithm first picks pair (5,1) and swaps it to produce 
array [1,5,4,2]. Next, it picks pair (5,4) and swaps it to produce array [1,4,5,2]. Next, pair (4,2) is picked and 
swapped to produce array [1,2,5,4], and finally, pair (5,4) is swapped to produce the final sorted 
array [1,2,4,5], so the number of swaps performed is 4.


---
Solution:
count inversions in an array


```
var (
num_index_pair [][]int
res []int
)

func countSmaller(nums []int) []int {
    if len(nums) == 0 {
        return []int{}
    }

    res = make([]int, len(nums))
    num_index_pair = make([][]int, len(nums))
    for i := 0; i < len(nums); i++ {
        num_index_pair[i] = []int{nums[i], i}
    }
    divide(num_index_pair)

    return res
}

func divide(num_index [][]int) [][]int {
    mid := len(num_index) / 2
    if len(num_index) > 1 {
        left := divide(num_index[:mid])
        right := divide(num_index[mid:])

        return conquer(left, right)
    } else {
        return num_index
    }
    
}

func conquer(left, right [][]int) [][]int {
    sort := make([][]int, 0)
    i := 0
    j := 0
    for i < len(left) && j < len(right) {
        if left[i][0] > right[j][0] {
            sort = append(sort, left[i])
            res[left[i][1]] += len(right) - j
            i ++
        } else {
            sort = append(sort, right[j])
            j ++
        }
    }
    
    for i < len(left) {
        sort = append(sort, left[i])
        i ++
    }
    
    for j < len(right) {
        sort = append(sort, right[j])
        j ++
    }
    
    return sort
}
```

Can also use fenwick (binary indexed tree) BIT
https://leetcode.com/problems/count-of-smaller-numbers-after-self/solutions/76625/golang-solution-using-binary-indexed-tree-with-detailed-explanation/

https://www.hackerearth.com/practice/notes/binary-indexed-tree-or-fenwick-tree/


```
func countSmaller(nums []int) []int {
	nlen := len(nums)

	sorted := make([]int, nlen)
	copy(sorted, nums)
	sort.Ints(sorted)

	mp := make(map[int]int)
	index := 0
	for i := range sorted {
		if _, ok := mp[sorted[i]]; !ok {
			mp[sorted[i]] = index
			index++
		}
	}

	bit := make(BIT, len(mp)+1)

	res := make([]int, nlen)
	for i := nlen - 1; i >= 0; i-- {
		res[i] = sum(bit, mp[nums[i]]-1)
		add(bit, mp[nums[i]], 1)
	}
	return res
}

type BIT []int

func add(b BIT, index int, value int) {
	i := index + 1
	for i < len(b) {
		b[i] += value
		i += i & (-i)
	}
}

func sum(b BIT, index int) int {
	sum := 0
	for i := index + 1; i > 0; i = i - i&(-i) {
		sum += b[i]
	}
	return sum
}
```