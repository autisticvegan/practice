
Note this problem is very easy if its immutable. But mutable version requires segment tree.  

```
type NumMatrix struct {
	Matrix [][]int
	Bit    BIT
}

func Constructor(matrix [][]int) NumMatrix {
	b := make(BIT, len(matrix)+1)
	for i := 1; i < len(matrix)+1; i++ {
		b[i] = make([]int, len(matrix[0])+1)
	}
	nm := NumMatrix{Bit: b, Matrix: matrix}
	for i := 0; i < len(matrix); i++ {
		for j := 0; j < len(matrix[0]); j++ {
			update(nm.Bit, i, j, matrix[i][j])
		}
	}
	return nm
}

func (this *NumMatrix) Update(row int, col int, val int) {
	update(this.Bit, row, col, val-this.Matrix[row][col])
	this.Matrix[row][col] = val
}

func (this *NumMatrix) SumRegion(row1 int, col1 int, row2 int, col2 int) int {
	area := sum(this.Bit, row2, col2)
	if row1 == 0 && col1 == 0 {
		return area
	} else if row1 == 0 {
		return area - sum(this.Bit, row2, col1-1)
	} else if col1 == 0 {
		return area - sum(this.Bit, row1-1, col2)
	}
	return area - sum(this.Bit, row2, col1-1) - sum(this.Bit, row1-1, col2) + sum(this.Bit, row1-1, col1-1)
}

type BIT [][]int

func update(bit BIT, row, col, val int) {
	for i := row + 1; i < len(bit); i += i & -i {
		for j := col + 1; j < len(bit[1]); j += j & -j {
			bit[i][j] += val
		}
	}
}

func sum(bit BIT, row, col int) int {
	res := 0
	for i := row + 1; i >= 1; i -= i & -i {
		for j := col + 1; j >= 1; j -= j & -j {
			res += bit[i][j]
		}
	}
	return res
}
```


Also brute force way that also passes on leetcode.  
```
type NumMatrix struct {
	sums   [][]int
	origin [][]int
}

func Constructor(matrix [][]int) NumMatrix {
	m, n := len(matrix), len(matrix[0])
	sums := make([][]int, m+1)
	for i := 0; i < m+1; i++ {
		sums[i] = make([]int, n+1)
	}
	for i := 1; i < m+1; i++ {
		for j := 1; j < n+1; j++ {
			sums[i][j] = sums[i-1][j] + sums[i][j-1] - sums[i-1][j-1] + matrix[i-1][j-1]
		}
	}
	return NumMatrix{sums: sums, origin: matrix}
}

func (this *NumMatrix) Update(row int, col int, val int) {
	m, n := len(this.sums), len(this.sums[0])
	diff := val - this.origin[row][col]
	this.origin[row][col] = val
	for i := row + 1; i < m; i++ {
		for j := col + 1; j < n; j++ {
			this.sums[i][j] += diff
		}
	}
}

func (this *NumMatrix) SumRegion(row1 int, col1 int, row2 int, col2 int) int {
	return this.sums[row2+1][col2+1] - this.sums[row1][col2+1] - this.sums[row2+1][col1] + this.sums[row1][col1]
}
```

Similar idea with C++  
```
class NumMatrix {
public:
    NumMatrix(vector<vector<int>> matrix) {
        int N = matrix.size();
        if(!N) return;
        int M = matrix[0].size();
        if(!M) return;
        vector<vector<int>> temp (N, vector<int>(M + 1));
        rec = temp;

        for(int i = 0; i < N; i++){
            for(int j = M - 1; j >= 0;  j--){
                if(j == M-1) rec[i][j] = matrix[i][j];
                else rec[i][j] = rec[i][j+1] + matrix[i][j];
            }
        }
    }
    
    void update(int row, int col, int val) {
        int pre = rec[row][col] - rec[row][col+1];
        for(int i = col; i >= 0; i--){
            rec[row][i] += (val - pre);
        }
    }
    
    int sumRegion(int row1, int col1, int row2, int col2) {
        int sum = 0;
        for(int i = row1; i <= row2; i++){
            sum += (rec[i][col1] - rec[i][col2 + 1]);
        }
        return sum;
    }
private:
    vector<vector<int>> rec;
};
 ```
























