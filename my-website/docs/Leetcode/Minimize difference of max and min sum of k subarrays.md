Given an array arr of non-negative integers. You need to split it into k contiguous subarrays such that the absolute difference between max sum and min sum is the smallest and output that difference.

Example:

Input: arr = [3, 4, 5, 3, 7, 2], k = 3
Output: 2
Explanation: Optimal split is subarray1 = [3, 4], subarray2 = [5, 3], subarray3 = [7, 2]
Min sum = 7 and max sum = 9, hence the answer is |7 - 9| = 2.

Harder version TODO: Do the same problem for a rotated array or 2d array, and also test the multi threaded approach

Solution:

Assume that you are assigning continuous section of board to each painter such that its total length 
must not exceed a predefined maximum, costmax. Then, you are able to find the number of painters 
that is required, x. Following are some key observations:
 
The lowest possible value for costmax must be the maximum element in A (name this as lo).
The highest possible value for costmax must be the entire sum of A, (name this as hi).
As costmax increases, x decreases. The opposite also holds true.
 
Now, the question translates directly into:
 
How do we use binary search to find the minimum of costmax while satisfying the condition x = k? The 
search space will be the range of [lo, hi].
 
Let us study using the example below to understand how this works:
Assume that A = { 100, 200, 300, 400, 500, 600, 700, 800, 900 },
and k = 3.
 
Since k is positive, we know that the highest possible costmax must be the sum of A, 4500. (ie, 
assigning all boards to one painter).
 
The lowest possible costmax must be the largest element in A, 900. This requires a total of six 
painters — The first painter paints {100, 200, 300}, second painter paints {400, 500} while the 
rest of them paints one board each).
 
Below is a simple conceptual illustration of how the search space looks like, with its corresponding 
x value (the required number of painters) pointing to costmax.
900        ...       4500
↑                     ↑
x=6                   x=1
 
Note that x decreases while costmax increases.
We want to find the minimum of costmax under the constraint of x = k.
900  ...  2700  ...  4500
↑          ↑          ↑
x=6        x=2        x=1
 
We choose the middle element, 2700, and find its corresponding x, which is 2.
Since x = k (which equals to 3), we can find a better minimum (ie, the real solution) in the lower half.
Therefore, we discard the upper half and continue searching in the lower half.
```
900  ...  1800  ...  2700
↑          ↑          ↑
x=6        x=3        x=2
```
The middle element now is 1800 and its corresponding x is 3, which is still = k.
We discard the upper half again and continue searching in the lower half.
```
900  ...  1350  ...  1800
↑          ↑          ↑
x=6        x=5        x=3
```
This time, the middle element is 1350 and its corresponding x is 5, which is > k.
We have to discard the lower half including the middle element itself, since x > k in that region (ie, 
no valid solution).
Here, read the phrase in bold “including the middle element itself“ again, as this is extremely important 
to maintain the invariant. Why?
Yes, that means the lower half including the value 1350 would be discarded.
We continue searching in the upper half (ie, in the range of [1351, 1800]).
 
…
 
After multiple successions of halving the search space, the final answer is 1700, and its corresponding
x is 3. This is also the minimum of costmax while maintaining the requirement x = k.
 
The complexity of this algorithm is O(N log ( ∑ Ai )), which is quite efficient. Furthermore, it does 
not require any extra space, unlike the DP solution which requires O(kN) space. This solution is also 
easier to code. Just be very careful while writing code for any variation of binary search, and think 
through all the corner cases while you code.

https://jackygao.wordpress.com/2014/09/04/the-painters-partition-problem-part-ii/

```
// You can edit this code!
// Click here and start typing.
package main

import "fmt"

func min(x, y int) int {
	if x < y {
		return x
	}
	return y
}

func max(x, y int) int {
	if x > y {
		return x
	}
	return y
}

func maxOfArr(arr []int) int {
	maxV := -9999
	for _, num := range arr {
		maxV = max(maxV, num)
	}

	return maxV
}

func sumOfArr(arr []int) int {
	res := 0
	for _, num := range arr {
		res += num
	}

	return res
}

func splitArrayKWays(arr []int, k int) int {
	low := maxOfArr(arr)
	high := sumOfArr(arr)
	maxV := 0
	minV := 0
	for low <= high {
		mid := low + (high-low)/2
		isPoss, theMin := isPossible(arr, k, mid)

		if isPoss {
			maxV = mid
			minV = theMin
			high = mid - 1
		} else {
			low = mid + 1
		}
	}

	return maxV - minV
}

func isPossible(arr []int, k, mid int) (bool, int) {

	count := 1
	sum := 0
	minV := 9999999
	for _, num := range arr {
		sum += num
		if sum > mid {
			minV = min(minV, sum-num)
			count++
			sum = num
		}
	}

	return count <= k, min(minV, sum)
}

func main() {

	nums1 := []int{18, 15, 20, 16, 17}
	nums2 := []int{60, 30, 50}

	fmt.Println(splitArrayKWays(nums1, 3))
	fmt.Println(splitArrayKWays(nums2, 2))

}

```