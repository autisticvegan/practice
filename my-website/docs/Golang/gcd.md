Many problems require a GCD function so here it is. Greatest Common Divisor
Stolen from https://github.com/pkorobeinikov/golang-example/edit/master/math/gcd.go

```
// GCDEuclidean calculates GCD by Euclidian algorithm.
func GCDEuclidean(a, b int) int {
	for a != b {
		if a > b {
			a -= b
		} else {
			b -= a
		}
	}

	return a
}

// GCDRemainderRecursive calculates GCD recursively using remainder.
func GCDRemainderRecursive(a, b int) int {
	if b == 0 {
		return a
	}
	return GCDRemainderRecursive(b, a%b)
}

// GCDRemainder calculates GCD iteratively using remainder.
func GCDRemainder(a, b int) int {
	for b != 0 {
		a, b = b, a%b
	}

	return a
}

```