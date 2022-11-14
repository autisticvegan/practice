
```

func calculate(s string) int {
    // 5 casse
    // num
    // +
    // -
    // (
    // )
    
    // for plus and minus, do the same thing
    // except change sign
    // as in, add sign * number, and reset
    // for digit, get 10 * num + curr num
    
    result := 0
    stack := []int{}
    sign := 1 // for dealing with neg nums
    currNum := 0
    
    for _, ch := range s {
        if unicode.IsDigit(ch) {
            val, _ := strconv.Atoi(string(ch))
            currNum = currNum * 10 + val
        } else if ch == '+' {
            result += sign * currNum
            currNum = 0
            sign = 1
        } else if ch == '-' {
            result += sign * currNum
            currNum = 0
            sign = -1
        } else if ch == '(' {
            //4 things
            // push result and sign
            // reset sign and result
            stack = append(stack, result)
            stack = append(stack, sign)
            sign = 1
            result = 0
        } else if ch == ')' {
            // 4 things
            // result += sign * num
            // number = 0
            // result * = last
            // result += last
            
            result += sign * currNum
            currNum = 0
            
            result *= stack[len(stack)-1]
            stack = stack[:len(stack)-1]
            
            result += stack[len(stack)-1]
            stack = stack[:len(stack)-1]
        }
        
    }
    
    if currNum != 0 {
        result += sign * currNum
    }
    return result
}
```