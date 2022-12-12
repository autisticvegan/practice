
Traverse Matrix Diagonally
```
// diagonal matrix

func getDiags(input [][]string) []int {

	string2Index := make(map[string]int)
	strings := []string{}

	startPoints := [][]int{}
	for i := len(input) - 1; i >= 0; i-- {
		startPoints = append(startPoints, []int{i, 0})
	}

	for i := 1; i < len(input[0]); i++ {
		startPoints = append(startPoints, []int{0, i})
	}

	for i, sp := range startPoints {

		currX := sp[0]
		currY := sp[1]
		tempStr := ""
		for {

			tempStr += input[currX][currY]

			if len(tempStr) == len(input) {
				string2Index[tempStr] = i
				strings = append(strings, tempStr)
				break
			}

			currX += 1
			currY += 1
			if currY >= len(input) || currX >= len(input[0]) {
				currX := sp[0]
				currY := sp[1]
			}

		}

	}

	sort.Strings(strings)

	result := []int{}

	for _, s := range strings {
		result = append(result, string2Index[s])
	}

	return result
}
```