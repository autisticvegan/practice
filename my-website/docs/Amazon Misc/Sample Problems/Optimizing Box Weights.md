- The intersection of A and B is null.
- The union A and B is equal to the original array.
- The number of elements in subset A is minimal.
- The sum of A's weights is greater than the sum of B's weights.
Return the subset A in increasing order where the sum of A's weights is greater than the sum of B's weights. If 
more than one subset A exists, return the one with the maximal total weight.

Example
n = 5
arr = [3, 7, 5, 6, 2]
The 2 subsets in arr that satisfy the conditions for A are [5, 7] and [6, 7] :
- A is minimal (size 2)
- Sum(A) = (5 + 7) = 12 > Sum(B) = (2 + 3 + 6) = 11
- Sum(A) = (6 + 7) = 13 > Sum(B) = (2 + 3 + 5) = 10
- The intersection of A and B is null and their union is equal to arr.
- The subset A where the sum of its weight is maximal is [6, 7].

```

func getSum(items []int) int {
    res := 0
    for _, x := range items {
        res += x
    }
    return res
}

func reverse(in []int) []int {
    for i := 0; i < len(in) / 2; i++ {
        t := in[i]
        in[i] = in[len(in) - i  - 1]
        in[len(in) - i - 1] = t
    }
    return in
}

func subsets(items []int) []int {

    sum := getSum(items)
    sort.Slice(items, func(i, j int) bool { return items[i] > items[j] })
    
    setA := []int{}
    runningTotal := 0
    for i := 0; i < len(items); i++ {
        
        setA = append(setA, items[i])
        runningTotal += items[i]
        sum -= items[i]

        if sum < runningTotal {
            break
        }

    }
    
    return reverrse(setA)
}

```