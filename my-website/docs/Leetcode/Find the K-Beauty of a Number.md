Find the K-Beauty of a Number

The k-beauty of an integer num is defined as the number of substrings of num when it is read as a string that meet the following conditions:

    It has a length of k.
    It is a divisor of num.

Given integers num and k, return the k-beauty of num.

Note:

    Leading zeros are allowed.
    0 is not a divisor of any value.

A substring is a contiguous sequence of characters in a string.

could also do things the string conv way but thats too easy

```

func divisorSubstrings(num int, k int) int {

    res := 0    
    pow := int(math.Pow(10, float64(k)))

    for curr := num; curr > 0; curr /= 10 {
        maybeDiv := curr % pow
        if maybeDiv != 0 && num % maybeDiv == 0 {
            res++
        }

        if curr / pow == 0 {
            break
        }
    }

    return res
}

```