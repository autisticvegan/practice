


Newton Raphsom
```
class Solution:
    def mySqrt(self, x: int) -> int:
        res = 1
        for i in range(20):
            temp = res
            res = temp - (temp**2 - x)/(2 * temp)
        return math.floor(res)
```

STandard solution of binary search
```
func mySqrt(x int) int {
    if x < 2 {
        return x
    }
    left, right := 1, x/2
    
    for left <= right {
        
        mid := (left+right)/2
        
        s := mid*mid
        if s == x {
            return mid
        }
        if s > x {
            right = mid - 1
        } else {
            left = mid + 1
        }
        
    }
    return right
}
```

Tricky disco
```
func mySqrt(x int) int {
	var out = 0

	for out*out < x {
		out++
	}

	if out*out > x {
		out--
	}

	return out
}
```