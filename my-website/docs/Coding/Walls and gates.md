Walls and Gates

You are given an m x n grid rooms initialized with these three possible values.

    -1 A wall or an obstacle.
    0 A gate.
    INF Infinity means an empty room. We use the value 231 - 1 = 2147483647 to represent INF as you may assume that the distance to a gate is less than 2147483647.

Fill each empty room with the distance to its nearest gate. If it is impossible to reach a gate, it should be filled with INF.

```
func wallsAndGates(rooms [][]int)  {
    for i := 0; i < len(rooms); i += 1 {
        for j := 0; j < len(rooms[0]); j += 1 {
            if rooms[i][j] == 0 {
                dfs(rooms, i, j, 0)
            }
        }
    }
}

func dfs(rooms [][]int, row, col, distance int) {
    var DIRECTIONS = [][]int{ {1, 0}, {0, 1}, {-1, 0}, {0, -1} }
    rooms[row][col] = distance
    
    for _, dir := range DIRECTIONS {
        nextRow, nextCol := row + dir[0], col + dir[1]
        
        if isInsideGrid(rooms, nextRow, nextCol) && distance + 1 < rooms[nextRow][nextCol] {
            dfs(rooms, nextRow, nextCol, distance + 1)
        }
    }
}

func isInsideGrid(rooms [][]int, row, col int) bool {
    return row >= 0 && row < len(rooms) && col >= 0 && col < len(rooms[0])
}
```