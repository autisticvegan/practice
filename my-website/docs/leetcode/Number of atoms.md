726. Number of Atoms

Given a string formula representing a chemical formula, return the count of each atom.

The atomic element always starts with an uppercase character, then zero or more lowercase letters, representing the name.

One or more digits representing that element's count may follow if the count is greater than 1. If the count is 1, no digits will follow.

    For example, "H2O" and "H2O2" are possible, but "H1O2" is impossible.

Two formulas are concatenated together to produce another formula.

    For example, "H2O2He3Mg4" is also a formula.

A formula placed in parentheses, and a count (optionally added) is also a formula.

    For example, "(H2O2)" and "(H2O2)3" are formulas.

Return the count of all elements as a string in the following form: the first name (in sorted order), followed by its count (if that count is more than 1), followed by the second name (in sorted order), followed by its count (if that count is more than 1), and so on.

```
func compute(formula string) map[string]int {

    // keep track of factor (starts at 1 is default)
    // keep track of current chem element
    // use stack to handle parens and past factors

    // 5 cases:
    // 1: it is a digit
    // 2: closing parens
    // 3: capital letter
    // 4: lowercase letter
    // 5: opening parens
    /*
    What to do in these cases:
    1: transform string digit to actual digit and record this factor
       also since you are looking forward, remember to reset index by -1
    2: push factor * stk.top onto the stack, reset factor to 1
    3: add the character, reverse the element, and put in the factor * the top value from stack
       also clear element and reset to 1
    4: add to the current element this character
    5: just pop off stack
    */

    stack := []int{1}
    currElem := ""
    factor := 1 
    stats := make(map[string]int)
    for i := 0; i < len(formula); i++ {
        c := rune(formula[i])
        if unicode.IsDigit(c) {
            val := 0
            expo := 1
            for unicode.IsDigit(c) {
                num, _ := strconv.Atoi(string(c))
                val += num * expo
                expo *= 10
                i++
                c = rune(formula[i])
            }
            factor = val
            i -= 1
        } else if c == ')' {
            stack = append(stack, factor * stack[len(stack)-1])
            factor = 1
        } else if c >= 'A' && c <= 'Z' {
            currElem += string(c)
            currElem = Reverse(currElem)
            stats[currElem] += factor * stack[len(stack)-1]
            factor = 1
            currElem = ""
        } else if c >= 'a' && c <= 'z' {
            currElem += string(c)
        } else {
            // c == '('
            stack = stack[:len(stack)-1]
        }

    }

    return stats
}
func Reverse(s string) string {
    runes := []rune(s)
    for i, j := 0, len(runes)-1; i < j; i, j = i+1, j-1 {
        runes[i], runes[j] = runes[j], runes[i]
    }
    return string(runes)
}

func countOfAtoms(formula string) string {
    
//reverse
//compute stats
//gather stats and sort
//return res

    formulaRev := Reverse(formula)
    stats := compute(formulaRev)
    res := ""

    keys := make([]string, len(stats))

    index := 0
    for k, _ := range stats {
        keys[index] = k
        index++
    }

    sort.Slice(keys, func(i, j int) bool {return keys[i] < keys[j]})

    for _, k := range keys {
        res += k
        if stats[k] > 1 {
            res += strconv.Itoa(stats[k])
        }
    }   

    return res
}
```