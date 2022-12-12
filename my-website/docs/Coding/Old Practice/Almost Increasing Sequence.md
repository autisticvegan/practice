
Some random Codesignal problem. 
```
func firstBadPair(sequence []int, n int) int {
	
	if 0 < n && n < len(sequence) - 1 {
		if sequence[n - 1] >= sequence[n + 1] {
	n-1
		}
	}

	for i := n + 1; i < len(sequence) - 1; i++ {
		if sequence[i] >= sequence[i + 1] {
			return i
		}
	}

	return -1
}

func almostIncreasing(sequence []int) bool {

	index := firstBadPair(sequence, -1)
	if index == -1 {
		return true
	}

	if firstBadPair(sequence, index + 1) == -1 {
		return true
	}

	if firstBadPair(sequence, index - 1) == -1 {
		return true
	}

	return false
}
```