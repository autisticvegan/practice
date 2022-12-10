
```
//left
func upperBound(arr []int, target int) int {
	l, r := 0, len(arr)
	for l < r {
		mid := (l + r) / 2
		if arr[mid] < target {
			l = mid + 1
		} else {
			r = mid
		}
	}
	return l
}

//right
func lowerBound(arr []int, target int) int {
	l, r := 0, len(arr)
	for l < r {
		mid := (l + r) / 2
		if arr[mid] > target {
			r = mid
		} else {
			l = mid + 1
		}
	}
	return l
}



func fullBloomFlowers(flowers [][]int, persons []int) []int {
    
    startsOfBlooms := []int{}
    endsOfBlooms := []int{}
    
    for _, f := range flowers {
        startsOfBlooms = append(startsOfBlooms, f[0])
        endsOfBlooms = append(endsOfBlooms, f[1])
    }
    
    sort.Ints(startsOfBlooms)
    sort.Ints(endsOfBlooms)
    
    
    result := []int{}

    // get the number of blooms that have started and ended at each spot
    for _, p := range persons {
        
        upBound :=  upperBound(endsOfBlooms, p) 
        loBound :=  lowerBound(startsOfBlooms, p)
        
        result = append(result, loBound - upBound)
    }
    
    
    
    
    return result
    
}

```