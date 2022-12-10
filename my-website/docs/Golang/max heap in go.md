

```
import (
  "container/heap"
)

type MaxHeap []int

func (h MaxHeap) Len() int           { return len(h) }
func (h MaxHeap) Less(i, j int) bool { return h[i] > h[j] }
func (h MaxHeap) Swap(i, j int)      { h[i], h[j] = h[j], h[i] }

func (h *MaxHeap) Push(x interface{}) {
	*h = append(*h, x.(int))
}

func (h *MaxHeap) Pop() interface{} {
  popped := (*h)[len(*h)-1]
  *h = (*h)[0:len(*h)-1]
	return popped
}

// ... use heap.Init(arr) and heap.Push(arr, x)

```