


```
type Node struct {
    Row int
    Col int
    K int
    Steps int
    Estimated int
}

func newNode(row, col, m, n, k, steps int) Node {
    distanceToEnd := distance(row, col, m, n)
    
    return Node{
        Row: row,
        Col: col,
        K: k,
        Steps : steps,
        Estimated: distanceToEnd + steps,
    }
}

func shortestPath(grid [][]int, k int) int {
    m := len(grid)
    n := len(grid[0])
    
    if distance(0, 0, m, n) <= k {
        return distance(0, 0, m, n)
    }
    
    dirs := [][]int{ {1,0}, {-1,0}, {0,1}, {0,-1} }
    visited := make(map[string]bool)
    init := newNode(0, 0, m, n, k, 0)
    
    minHeap := &MinHeap{}
    heap.Push(minHeap, init)
    visited[key(init)] = true
    
    for minHeap.Len() > 0 {
        node := heap.Pop(minHeap).(Node)
        
        remainingDistance := node.Estimated - node.Steps
        if remainingDistance <= node.K {
            return node.Estimated
        }
        
        for _, dir := range dirs {
            row := node.Row + dir[0]
            col := node.Col + dir[1]
            
            if row < 0 || row == m || col < 0 || col == n {
                continue
            }
            
            nextK := node.K - grid[row][col]
            next := newNode(row, col, m, n, nextK, node.Steps+1)
            
            if nextK >= 0 && !visited[key(next)] {
                visited[key(next)] = true
                heap.Push(minHeap, next)
            }
        }
    }
    
    return -1
}

func distance(row, col, m, n int) int {
    return m + n - row - col - 2
}

func key(node Node) string {
    return strconv.Itoa(node.Row) + "-" + strconv.Itoa(node.Col) + "-" + strconv.Itoa(node.K)
}

type MinHeap []Node

func (h MinHeap) Len() int {
    return len(h)
}

func (h MinHeap) Less(i int, j int) bool {
    return h[i].Estimated < h[j].Estimated
}
                          
func (h MinHeap) Swap(i int, j int) {
    h[i], h[j] = h[j], h[i]
} 
                          
func (h *MinHeap) Push(a interface{}) {
    *h = append(*h, a.(Node))
}

func (h *MinHeap) Pop() interface{} {
    l := len(*h)
    res := (*h)[l - 1]
    *h = (*h)[:l - 1]
    return res
}
```

