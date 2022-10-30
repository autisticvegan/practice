1046. Last Stone Weight

You are given an array of integers stones where stones[i] is the weight of the ith stone.

We are playing a game with the stones. On each turn, we choose the heaviest two stones and smash them together. Suppose the heaviest two stones have weights x and y with x <= y. The result of this smash is:

    If x == y, both stones are destroyed, and
    If x != y, the stone of weight x is destroyed, and the stone of weight y has new weight y - x.

At the end of the game, there is at most one stone left.

Return the weight of the last remaining stone. If there are no stones left, return 0.

```
func lastStoneWeight(stones []int) int {
  h := (*MaxHeap)(&stones)
  heap.Init(h)

  for h.Len() > 1 {
    s1 := heap.Pop(h).(int)
    s2 := heap.Pop(h).(int)
    newS := int(math.Abs(float64(s1 - s2)))
    if newS != 0 {
      heap.Push(h, newS)
    }
  }

  if h.Len() == 1 {
    return (*h)[0]
  }

  return 0
}

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
```