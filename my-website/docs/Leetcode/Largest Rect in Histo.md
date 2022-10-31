

```
func max(i, j int) int {
    if (i >= j) {return i} else {return j}
}
func largestRectangleArea(heights []int) int {
    stack := make([][]int, 0);
    stack = append(stack, []int{-1, 0});
    result := 0;
    
    for right, h := range append(heights, 0) {
        // pop if the top of the stack is larger than the current bar's height
        // such that it wouldnt make any valid rectangles after this
        for h < stack[len(stack)-1][1] && len(stack) > 1{
            h_left := stack[len(stack)-1][1]
            stack = stack[:len(stack)-1] // pop
            left := stack[len(stack)-1][0] // get the left most index
            rec_area := (right - left - 1) * h_left;
            result = max(result, rec_area);
        }
        if len(stack) > 0 && h == stack[len(stack)-1][1] {
            // pop previous since would not make difference but add computational time
            stack = stack[:len(stack)-1]; 
        }
        stack = append(stack, []int{right, h});
    }
    return result
}
```

See also [Wizards](./Sum%20of%20total%20strength%20of%20wizards.md)