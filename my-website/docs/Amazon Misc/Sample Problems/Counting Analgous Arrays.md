An array is said to be analogous to the secret array if all of the following conditions are true:
- The length of the array is equal to the length of the secret array.
- Each integer in the array lies in the interval [lowerBound, upperBound].
- The difference between each pair of consecutive integers of the array must be equal to the 
difference between the respective pair of consecutive integers in the secret array. 
```
In other 
words, let the secret array be [s[0], s[1],...s[n-1]]and let the analogous array be [a[0],a[1],...a[n1]], then (a[i-1] - a[i]) must be equal to (s[i-1] - s[i]) for each i from 1 to n-1.
```
Given the value of the integers lowerBound and upperBound, inclusive, and the array of 
differences between each pair of consecutive integers of the secret array, find the number of 
arrays that are analogous to the secret array. If there is no array analogous to the secret array, 
return 0.
For example:
consecutiveDifference = [-2, -1, -2, 5]
lowerBound=3
upperBound=10
The logic to create an analogous array starting from the lower bound is:
```
Start with a value of 3.
Subtract consecutiveDistances[0], 3 - (-2) = 5
Subtract consecutiveDistances[1], 5 - (-1) = 6
Subtract consecutiveDistances[2], 6 - (-2) = 8
Subtract consecutiveDistances[3], 8 - 5 = 3
Note that none of the values is out of bounds. All possible analogous arrays are:
```
[3, 5, 6, 8, 3]
[4, 6, 7, 9, 4]
[5, 7, 8, 10, 5]
The answer is 3.
Function Description 
Complete the function countAnalogousArrays in the editor below.
countAnalogousArrays has the following parameter(s):
 int consecutiveDifference[]: the differences between each pair of consecutive integers in the 
secret array
 int lowerBound: an integer
 int upperBound: an integer
Returns:
 int: the number of arrays that are analogous to the secret array
 
Constraints 
- -109 ≤ lowerBound ≤ upperBound ≤ 109
- 1 ≤ n ≤ 105
- -2*109 ≤ consecutiveDifference[] ≤ 2*109

Go solution
```
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

func countAnalArrs(nums []int, high, low int) int {

    maxVal := -9999999999
    minVal := 999999999
    runningTotal := 0
    for _, x := range nums {
        runningTotal += x * -1
        maxVal = max(runningTotal, maxVal)
        minVal = min(runningTotal, minVal)
    }

    // high + mindiff - lower - maxdiff
    // num1 = 20 if someBoolValue else num1
    // num1 someBoolVal ? 20 : num1
    /*
    maxvalidupperbound = upperBound + mindiff if upperBound+mindiff < upperBound else upperBound
    minvalidlowerbound = lowerBound + maxdiff if lowerBound + maxdiff > lowerBound else lowerBound

    maxValidUpperBound = (upperBound+minDiff < upperBonud) ? upperbound + mindiff : upperbound
    minValidUpperBound = lowerBound + maxdiff > lowerBound ? lowerBound + maxDiff : lowerBound

    */

    return (high - low) - (maxVal - minVal) + 1
}


```

