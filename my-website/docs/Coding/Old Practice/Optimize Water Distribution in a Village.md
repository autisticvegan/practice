
Optimize Water Distribution in a Village
Leetcode 1168

```
type EdgeCost struct {
	from, to int
	cost     int
}



func OptimizeWaterDistributionInAVillage(wells []int, pipes [][]int) int {
	// minimize cost between building a well vs connecting with pipes
	// tricks:
	// MST
	// use an extra 0 node for well costs
	// weight union find

	nodeCount = len(wells)
	edgeCosts := []EdgeCost{}

	for i := 1; i <= len(wells); i++ {
		edgeCosts = append(edgeCosts, EdgeCost{from: 0, to: i, cost: wells[i-1]})
	}

	for i := 0; i < len(pipes); i++ {
		edgeCosts = append(edgeCosts, EdgeCost{pipes[i][0], pipes[i][1], pipes[i][2]})
	}

	sort.Slice(edgeCosts, func(i,j int) bool {
		return edgeCosts[i].cost < edgeCosts[j].cost
	})


	minCost := 0

	// https://github.com/theodesp/unionfind

	uf := unionfind.New(nodeCount)
	for _, e := range edgeCosts {
		if uf.Connected(e.from, e.to) {
			continue
		}
		minCost += e.cost
		uf.Union(e.from, e.to)
		nodeCount--
		if nodeCount == 0 {
			return minCost
		}
	}

	return minCost
}
```