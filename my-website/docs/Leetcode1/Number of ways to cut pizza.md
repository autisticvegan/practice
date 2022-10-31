MOST COMMON PROBLEM FOR TIKTOK

i,j,k = coords and k cuts
prefix sum


```
const M = int(1e9 + 7)

var dp [][][]int 
var a [][]int 
var n int
var m int 

func getSum(i, j, u, v int) int {

	// get sum of tomatoes inside rec (i, j) -> (u, v)
	return a[u][v] - a[u][j - 1] - a[i - 1][v] + a[i - 1][j - 1]
}

func DP(last_row, last_col, k int) int {

	// use enough slice
	if (k == 0) {
		// if the rest having larger than 1 tomato
		if getSum(last_row, last_col, n, m) > 0 {
			return 1
		}
		return 0
	}

	// if the rest is not a sub-rec  
	if last_col == m + 1 || last_row == n + 1 {
		return 0
	}

	// if solution have been already exist
	if dp[last_row][last_col][k] != -1 {
		return dp[last_row][last_col][k]
	}

	ans := 0
	
	// slice row
	for i := last_row; i <= n; i++ {
		if getSum(last_row, last_col, i, m) > 0 {
			ans = (ans + DP(i + 1, last_col, k - 1)) % M
		}
	}

	// slice col
	for i := last_col; i <= m; i++ {
		if getSum(last_row, last_col, n, i) > 0 {
			ans = (ans + DP(last_row, i + 1, k - 1)) % M
		}
	}

	dp[last_row][last_col][k] = ans
	return ans

}

func ways(pizza []string, k int) int {

	// number of row
	n = len(pizza)
	// number of col
    m = len(pizza[0])

	// init a
	a = make([][]int, n + 1)
	for i := 0; i < n + 1; i++ {
		a[i] = make([]int, m + 1)
	}

	// init dp
	dp = make([][][]int, n + 1)
	for i := 0; i < n + 1; i++ {
		dp[i] = make([][]int, m + 1)
		for j := 0; j < m + 1; j++ {
			dp[i][j] = make([]int, k + 1)
			for x := 0; x < k + 1; x++ {
				dp[i][j][x] = -1
			}
		}
	}

	// calc prefix sum of matrix 2D a ('A' is 1, '.' is 0)
	for i := 1; i <= n; i++ {
		for j := 1; j <= m; j++ {
			if pizza[i - 1][j - 1] == 'A' {
				a[i][j] = a[i - 1][j] + a[i][j - 1] - a[i - 1][j - 1] + 1
			} else {
				a[i][j] = a[i - 1][j] + a[i][j - 1] - a[i - 1][j - 1]
			}
		}
	}

	return DP(1, 1, k - 1)

}
```