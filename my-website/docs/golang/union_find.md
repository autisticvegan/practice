In many interview questions, we need to use UnionFind, but we cannot import github packages, so here is a handy copy-pasteable implementation that was made by a person.

shamelessly stolen from https://github.com/AbhiAgarwal/go-unionfind/blob/master/unionfind.go

```
type UnionFind struct {
	P, Rank, SetSize []int
	NumSets          int
}

func NewUnionFind() *UnionFind {
	return &UnionFind{}
}

func (u *UnionFind) UnionFind(n int) {
	u.NumSets = n
	u.Rank = make([]int, n)
	u.SetSize = make([]int, n)
	u.P = make([]int, n)
	for i := 0; i < n; i++ {
		u.SetSize[i] = 1
		u.Rank[i] = 0
		u.P[i] = i
	}

}

func (u *UnionFind) FindSet(i int) int {
	if u.P[i] == i {
		return i
	} else {
		u.P[i] = u.FindSet(u.P[i])
		return u.P[i]
	}
}

func (u *UnionFind) IsSameSet(i, j int) bool {
	if u.FindSet(i) == u.FindSet(j) {
		return true
	}
	return false
}

func (u *UnionFind) UnionSet(i, j int) {
	if !u.IsSameSet(i, j) {
		u.NumSets = u.NumSets - 1
		x := u.FindSet(i)
		y := u.FindSet(j)
		if u.Rank[x] > u.Rank[j] {
			u.P[y] = x
			u.SetSize[x] += u.SetSize[y]
		} else {
			u.P[x] = y
			u.SetSize[y] += u.SetSize[x]
			if u.Rank[x] == u.Rank[y] {
				u.Rank[y] = u.Rank[y] + 1
			}
		}
	}
	return
}

func (u *UnionFind) NumDisjointSets() int {
	return u.NumSets
}

func (u *UnionFind) SizeOfSet(i int) int {
	return u.SetSize[u.FindSet(i)]
}
```