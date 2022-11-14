
brute force:
bfs from each land to all houses
improved: bfs from each house to empty land

more improved: Algorithm Optimized

    - For each grid[i][j] that is equal to 1, start a BFS. During the BFS:
        1. All 4-directionally adjacent grid cells with values equal to emptyLandValue are valid.
        2. Visit them one by one and store the distances of these cells from the source in a total matrix.
        3. Decrease the value of visited cells by 1.
    - After each BFS traversal, decrement emptyLandValue by 1.
    - Before we start a BFS call for a house, we set minDist equal to INT_MAX.
    - Then we will traverse all of the empty land cells with values equal to emptyLandValue
    - After the last BFS traversal, if the minimum distance equals INT_MAX, then there has not been any cell that can be reached by all the houses, so return -1.
    - Otherwise, return the minimum distance minDist.



```
func shortestDistance(grid [][]int) int {
    bds := findBuildings(&grid)
    rest := emptyGrid(&grid)
    
    for i := 0; i< len(bds); i++ {
        bd := bds[i]
        bfs(bd, &grid, &rest, -i)
    }
    
    flag := -len(bds)
    return countBest(&grid, &rest, flag)
}

func countBest(g, r *[][]int, flag int) int {
    grid, rst := *g, *r
    rc, cc := len(grid), len(grid[0])
    res := math.MaxInt64
    
    for i := 0; i< rc; i++ {
        for j := 0; j < cc; j++ {
            if grid[i][j] != flag {
                continue
            }
            
            res = minOf(res, rst[i][j]) 
        }
    }
    
    if res == math.MaxInt64{
        return -1
    }
    return res
}


func bfs(start [2]int, g *[][]int, c *[][]int, flag int) {
    grid, count := *g, *c
    rc, cc := len(grid), len(grid[0])
    dirs := [][2]int{
        [2]int{1,0},
        [2]int{-1,0},
        [2]int{0,1},
        [2]int{0,-1},
    }
    queue := [][2]int{start}
    step := 0
    for len(queue) > 0 {
        newQueue := [][2]int{}
        for len(queue) > 0 {
            top := queue[0]
            queue = queue[1:]
            
            count[top[0]][top[1]] += step
            
            for _,d := range dirs {
                newR, newC := top[0] + d[0], top[1] + d[1]
                if newR >= 0 && newR < rc && newC >=0 && newC < cc && grid[newR][newC] == flag {
                    grid[newR][newC]--
                    newQueue = append(newQueue, [2]int{newR, newC})
                }
            }
        }
        step++
        queue = newQueue
    }
    
}

func minOf(a,b int) int {
    if a < b {
        return a
    }
    return b
}

func emptyGrid(g *[][]int) [][]int {
    grid := *g
    res := make([][]int, len(grid))
    
    for i := 0; i< len(res); i++ {
        row := make([]int, len(grid[0]))
        res[i] = row
    }
    
    return res
}

func findBuildings(g *[][]int) [][2]int{
    grid := *g
    
    res := [][2]int{}
    for i:= 0 ; i< len(grid); i++ {
        for j := 0; j < len(grid[0]); j++ {
            if grid[i][j] == 1 {
                res = append(res, [2]int{i,j})
            }
        }
    }
    
    return res
}
```