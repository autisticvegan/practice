399. Evaluate Division

You are given an array of variable pairs equations and an array of real numbers values, where equations[i] = [Ai, Bi] and values[i] represent the equation Ai / Bi = values[i]. Each Ai or Bi is a string that represents a single variable.

You are also given some queries, where queries[j] = [Cj, Dj] represents the jth query where you must find the answer for Cj / Dj = ?.

Return the answers to all queries. If a single answer cannot be determined, return -1.0.

Note: The input is always valid. You may assume that evaluating the queries will not result in division by zero and that there is no contradiction.

 
```
Example 1:

Input: equations = [["a","b"],["b","c"]], values = [2.0,3.0], queries = [["a","c"],["b","a"],["a","e"],["a","a"],["x","x"]]
Output: [6.00000,0.50000,-1.00000,1.00000,-1.00000]
Explanation: 
Given: a / b = 2.0, b / c = 3.0
queries are: a / c = ?, b / a = ?, a / e = ?, a / a = ?, x / x = ?
return: [6.0, 0.5, -1.0, 1.0, -1.0 ]

Example 2:

Input: equations = [["a","b"],["b","c"],["bc","cd"]], values = [1.5,2.5,5.0], queries = [["a","c"],["c","b"],["bc","cd"],["cd","bc"]]
Output: [3.75000,0.40000,5.00000,0.20000]

Example 3:

Input: equations = [["a","b"]], values = [0.5], queries = [["a","b"],["b","a"],["a","c"],["x","y"]]
Output: [0.50000,2.00000,-1.00000,-1.00000]
```

Can do bfs, or floyd-warshall, or disjoint set


Disjoint Set:
```

func calcEquation(equations [][]string, values []float64, queries [][]string) []float64 {
	set := &stringSet{make(map[string]string, 0), make(map[string]float64, 0)}
	res := make([]float64, len(queries))
	for idx, eq := range equations {
		set.union(eq[0], eq[1], values[idx])
	}
	for idx, que := range queries {
		pX, vX, bX := set.find(que[0])
		pY, vY, bY := set.find(que[1])
		if bX == true || bY == true || pX != pY {
			res[idx] = -1
			continue
		}
		res[idx] = vX / vY
	}
	return res
}

type stringSet struct {
	parent map[string]string
	value  map[string]float64
}

func (s *stringSet) init(xs ...string) {
	for _, x := range xs {
		if _, ok := s.parent[x]; ok {
			continue
		}
		s.parent[x] = x
		s.value[x] = 1.0
	}
}

func (s *stringSet) find(x string) (parent string, value float64, err bool) {
	if _, ok := s.parent[x]; !ok {
		return x, -1, true
	}
	if x != s.parent[x] {
		px, vx, _ := s.find(s.parent[x])
		s.parent[x] = px
		s.value[x] *= vx
	}
	return s.parent[x], s.value[x], false
}

func (s *stringSet) union(a, b string, v float64) {
	s.init(a, b)

	pa, va, _ := s.find(a)
	pb, vb, _ := s.find(b)
	if pa != pb {
		s.parent[pa] = pb
		s.value[pa] = v * vb / va
	}
}
```

BFS:
```
type node struct { // variables
    edges []*edge // directed
    name string
}

type edge struct {
    target *node
    multiplier float64
}

type parentMulti struct {
    parent *node
    multiplier float64
}

func bfs(source, target *node) (float64, bool) {
    if source == nil || target == nil {
        return 0.0, false
    }
    
    parents := make(map[*node]parentMulti)
    
    q := []*node{ source }
    found := false
    
    for len(q) > 0 {
        newQ := []*node{}
        for _, n := range(q) {
            for _, e := range(n.edges) {
                if parents[e.target].parent != nil {
                    continue
                }
                parents[e.target] = parentMulti{ n, e.multiplier }
                if e.target == target {
                    found = true
                    break
                }
                newQ = append(newQ, e.target)
            }
        }
        q = newQ
    }
    if found {
        ret := 1.0
        cursor := target
        for cursor != source {
            ret *= parents[cursor].multiplier
            cursor = parents[cursor].parent
        }
        return ret, true
    }
    return 0.0, false
    
}

func calcEquation(equations [][]string, values []float64, queries [][]string) []float64 {
    nodesCache := make(map[string]*node)
    
    // build graph
    for i := range(equations) {
        n1 := nodesCache[equations[i][0]]
        if n1 == nil {
            n1 = new(node)
            nodesCache[equations[i][0]] = n1
        }
        n2 := nodesCache[equations[i][1]]
        if n2 == nil {
            n2 = new(node)
            nodesCache[equations[i][1]] = n2
        }
        n1ToN2 := &edge{n2, values[i]}
        n1.edges = append(n1.edges, n1ToN2)
        n2ToN1 := &edge{n1, 1.0/values[i]}
        n2.edges = append(n2.edges, n2ToN1)
    }
    
    ret := []float64{}
    
    for _, q := range(queries) {
        if value, ok := bfs(nodesCache[q[0]], nodesCache[q[1]]); ok {
            ret = append(ret, value)
        } else {
            ret = append(ret, -1.0)
        }
    }
    
    return ret
}
```


Floyd Warshall:
```
func calcEquation(equations [][]string, values []float64, queries [][]string) []float64 {
    dist := make(map[string]map[string]float64)
    for i, e := range equations {
        from, to := e[0], e[1]
        
        if dist[from] == nil {
            dist[from] = make(map[string]float64)
        }
        if dist[to] == nil {
            dist[to] = make(map[string]float64)
        }
        
        dist[from][to] = values[i]
        dist[to][from] = 1 / values[i]
        dist[from][from], dist[to][to] = 1, 1
    }
    for k, d := range dist {
        for k1 := range d {
            for k2 := range d {
                dist[k1][k2] = dist[k1][k] * dist[k][k2]
            }
        }
    }
    
    result := []float64{}
    for _, q := range queries {
        from, to := q[0], q[1]
        _, okFrom := dist[from]
        _, okTo := dist[to]
        
        if okFrom && okTo && dist[from][to] > 0 {
            result = append(result, dist[from][to])
        } else {
            result = append(result, -1)
        }
    }

    return result
}
```

---
tags: [Floyd-Warshall, BFS, Disjoint-Set] 
---