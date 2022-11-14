
Largest Plus Sign

You are given an integer n. You have an n x n binary grid grid with all values initially 1s except for some indices given in the array mines. The ith element of the array mines is defined as mines[i] = [xi, yi] where grid[xi][yi] == 0.

Return the order of the largest axis-aligned plus sign of 1s contained in grid. If there is none, return 0.

An axis-aligned plus sign of 1s of order k has some center grid[r][c] == 1 along with four arms of length k - 1 going up, down, left, and right, and made of 1s. Note that there could be 0s or 1s beyond the arms of the plus sign, only the relevant area of the plus sign is checked for 1s.

dp with longest line extending that way
```
func orderOfLargestPlusSign(n int, mines [][]int) int {
	zeros := make(map[[2]int]bool, len(mines))
	for _, mine := range mines {
		zeros[[2]int{mine[0], mine[1]}] = true
	}

	dp := make([][]int, n)
	for i := 0; i < n; i++ {
		dp[i] = make([]int, n)
	}

	helper := func(count *int, i, j int) int {
		if zeros[[2]int{i, j}] {
			*count = 0
		} else {
			*count++
		}

		return *count
	}

	for i := 0; i < n; i++ {
		count := 0
		for j := 0; j < n; j++ {
			dp[i][j] = helper(&count, i, j)
		}

		count = 0
		for j := n - 1; j >= 0; j-- {
			dp[i][j] = min(helper(&count, i, j), dp[i][j])
		}
	}

	max := 0
	for i := 0; i < n; i++ {
		count := 0
		for j := 0; j < n; j++ {
			dp[j][i] = min(helper(&count, j, i), dp[j][i])
		}

		count = 0
		for j := n - 1; j >= 0; j-- {
			x := min(helper(&count, j, i), dp[j][i])
			if x > max {
				max = x
			}
		}
	}

	return max
}

func min(a, b int) int {
	if a < b {
		return a
	}
	return b
}
```