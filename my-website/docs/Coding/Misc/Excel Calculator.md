Basic Excel Calculator

Methods:
set(id: string, expression: string[]): void
get(id: string): int

Note:
- expression values will either be integer strings like ('1', '2', '12') or cell ids like ('A1', 'B1', 'C12'), where cells are a character followed by an integer value

Example:
set('A1', ['1']) -> A1 = 1
set('B1', ['1', 'A1']) -> B1 = 2 
set('A1', ['3']) -> A1 = 3 AND B1 = 4 because all cells MUST be updated when the cell in their 'expression' is updated
set('C1', ['0', 'A1', 'B1'])

Note in the example that A1 does not care about B1, but B1 DOES care about A1
Thus any time we touch A1, we must also touch B1. However, the opposite does not hold.


See also: https://leetcode.com/problems/design-excel-sum-formula

// observer pattern

```
package main

import (
	"fmt"
	"strconv"
)

type Cell struct {
	baseValue int             // we need the base value because when we update, we need to keep it static
	observing map[string]bool // to avoid duplicates, we have a set
	delta     int             // the delta will be the sum of values coming from other cells, which will be added to the baseValue
}

func (e *ExcelCalculator) Update(start string, val int) {

	visitedSet := make(map[string]bool)
	q := []string{start}

	for len(q) != 0 {

		node := q[0]
		q = q[1:]

		if _, ok := visitedSet[node]; ok {
			//cycle detected

			break
		}

		visitedSet[node] = true
		e.grid[node].delta = val
		fmt.Println("node ", node, "'s delta is now ", e.grid[node].delta)
		for k, v := range e.grid[node].observing {
			if v == true {
				q = append(q, k)
			}
		}
	}

	// if cycle was detected, set value to -1
	if len(q) != 0 {
		e.grid[start].baseValue = -1
	}
}

func (e *ExcelCalculator) Set(key string, input []string) {

	intVal, _ := strconv.Atoi(input[0])
	//beingObserved := make(map[string]bool)
	for i := 1; i < len(input); i++ {
		//fmt.Println(input[i])
		_, ok := e.grid[input[i]]
		if !ok {
			e.grid[input[i]] = &Cell{
				observing: make(map[string]bool),
			}
		}

		cell := e.grid[input[i]] // we now know cell is not nil
		cell.observing[key] = true
	}

	sum := intVal
	for i := 1; i < len(input); i++ {
		sum += e.grid[input[i]].baseValue + e.grid[input[i]].delta
	}

	if _, ok := e.grid[key]; ok {
		fmt.Println(key, " already exists, updating it")
		mpCopy := e.grid[key].observing
		e.grid[key] = &Cell{
			baseValue: intVal,
			delta:     sum - intVal,
			observing: mpCopy,
		}

		//now, update all these that are observing with this new sum
		for k, v := range e.grid[key].observing {
			fmt.Println("Updating ", k, " because it is observed by ", key, " which has a base of ", intVal)
			if v == true {
				e.Update(k, sum)
			}
		}
	} else {
		e.grid[key] = &Cell{
			baseValue: intVal,
			delta:     sum - intVal,
			observing: make(map[string]bool),
		}
	}
}

func (e ExcelCalculator) Get(key string) int {
	if v, ok := e.grid[key]; ok {
		fmt.Println("GET ", key, " baseValue:", v.baseValue, " delta:", v.delta)
		return v.baseValue + v.delta
	}
	return -1
}

type ExcelCalculator struct {
	grid map[string]*Cell
}

func main() {

	e := ExcelCalculator{
		grid: make(map[string]*Cell),
	}
	e.Set("A1", []string{"1"})
	fmt.Println("A1 is ", e.Get("A1"))
	e.Set("B1", []string{"1", "A1"}) // A1 observes B1
	fmt.Println("B1 is now ", e.Get("B1"))
	fmt.Println("A1 is now ", e.Get("A1"))
	e.Set("A1", []string{"3"})
	fmt.Println("B1 is now ", e.Get("B1"))
	e.Set("C1", []string{"0", "A1", "B1"})
	fmt.Println("C1 is ", e.Get("C1"))
}


```