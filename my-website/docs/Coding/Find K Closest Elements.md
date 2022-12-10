Find K Closest Elements

```
Given a sorted integer array arr, two integers k and x, return the k closest integers to x in the array. The result should also be sorted in ascending order.

An integer a is closer to x than an integer b if:

    |a - x| < |b - x|, or
    |a - x| == |b - x| and a < b

```

```

func findClosestElements(arr []int, k int, x int) []int {

    low := 0
    high := len(arr) - k

    for low < high {
        mid := (low + high) / 2
        // if the gap is bigger on the left than the right, move up left
        if x - arr[mid] > arr[mid + k] - x {
            low = mid + 1
        } else {
            high = mid 
        }
    }

    return arr[low:low+k]
}


```