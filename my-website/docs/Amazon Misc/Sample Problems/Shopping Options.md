




```

// returns 0 - 3 based on which is longest
func getLongest(a, b, c, d []int) int {

// 1 and 2
    f := max(len(a), len(b))

// 3 and 4
    s := max(len(c), len(d))

    fi := max(f, s)

    if fi == len(a) {
        return 0
    } else if fi == len(b) {
        return 1
    } else if fi == len(c) {
        return 2
    }
    return 3
}

func max(x,y int) int {
    if x > y {
        return x
    }
    return y
}

func getOptions(options [][]int) int {

    // sort all arrays
    // use greedy approach
    // n^3 - fix first 3 points, with early exit in case its too much, and then on have index to values
    // can also use the longest one

    // find longest one
    longest := getLongest(options...)

    // sort and key longest
    
    
}


```