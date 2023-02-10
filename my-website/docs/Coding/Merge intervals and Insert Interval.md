- merge intervals (extremely common problem)


`
func max(x, y int) int {
    
    if x >= y {
        return x
    }else{
        return y
    }
    
}

//---------------------


func merge(intervals [][]int) [][]int {

    // predefined constant for start (left endpoint), as well as end (right endpoint)
    const START, END = 0, 1
    
    result := make( [][]int, 0);
    
    sort.Slice(intervals, func(a, b int) bool {
        return (intervals[a][0] < intervals[b][0]) || ( (intervals[a][0] == intervals[b][0]) && (intervals[a][1] < intervals[b][1]) )
    })
    
    for _, curInterval := range intervals{
        
        if ( len(result) == 0 ) || ( result[len(result)-1][END] < curInterval[START] ){
            
            // no overlapping
            result = append(result, curInterval)
            
        }else{
            
            // has overlapping
            // merge with previous interval
            result[len(result)-1][END] = max( result[len(result)-1][END], curInterval[END] )
        }
        
    }
    
    return result
}
`


- Insert Interval - similar problem but input is sorted so you can use bin search.
- if interviewer says to reuse code, you can just call the above function then iterate.

`
func binarySearch(intervals [][]int, val int) int {
	var (
		left  = 0
		right = len(intervals) - 1
		mid   = right / 2
	)

	for left <= right {
		if val < intervals[mid][0] {
			right = mid - 1
		} else if val > intervals[mid][1] {
			left = mid + 1
		} else {
			return mid
		}

		mid = (right-left)/2 + left
	}

	return left
}

func intervalInclude(interval []int, val int) bool {
	return interval[0] <= val && interval[1] >= val
}

func insert(intervals [][]int, newInterval []int) [][]int {
	var (
		startIndex = binarySearch(intervals, newInterval[0])
		endIndex   = binarySearch(intervals, newInterval[1])
		result     = append(make([][]int, 0, startIndex+len(intervals)-endIndex+1), intervals[:startIndex]...)
	)

	if startIndex != len(intervals) && intervalInclude(intervals[startIndex], newInterval[0]) {
		newInterval[0] = intervals[startIndex][0]
	}

	if endIndex != len(intervals) && intervalInclude(intervals[endIndex], newInterval[1]) {
		newInterval[1] = intervals[endIndex][1]
	}

	result = append(result, newInterval)

	if endIndex != len(intervals) && intervalInclude(intervals[endIndex], newInterval[1]) {
		endIndex++
	}

	return append(result, intervals[endIndex:]...)
}
`