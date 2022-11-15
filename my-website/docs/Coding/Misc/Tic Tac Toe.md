# Tic Tac Toe

Make a tic tac toe game between 2 AI's that place random moves, and return the result. Board size could be N.

Trick: Don't actually need a board (lol)

```

func main() {
    
}

func shuffle(input []int) []int {
	rand.Seed(time.Now().UnixNano())
	rand.Shuffle(len(a), func(i, j int) { a[i], a[j] = a[j], a[i] })
}

// use division for rows, mod for cols, when putting everything in one row

```


```
class TicTacToe {
private:
    //count parameter: player 1 + : player 2: -
    vector<int> rowJudge;
    vector<int> colJudge;
    int diag, anti;
    int total;
public:
    /** Initialize your data structure here. */

    TicTacToe(int n):total(n), rowJudge(n), colJudge(n),diag(0),anti(0){}

    int move(int row, int col, int player) {
        int add = player == 1 ? 1 : -1;
        diag += row == col ? add : 0;
        anti += row == total - col - 1 ? add : 0;
        rowJudge[row] += add;
        colJudge[col] += add;
        if(abs(rowJudge[row]) == total || abs(colJudge[col]) == total || abs(diag) == total || abs(anti) == total) 
            return player;
        return 0;
    }
};
```