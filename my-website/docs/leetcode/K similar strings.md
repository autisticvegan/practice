854. K-Similar Strings
     
Strings s1 and s2 are k-similar (for some non-negative integer k) if we can swap the positions of two letters in s1 exactly k times so that the resulting string equals s2.

Given two anagrams s1 and s2, return the smallest k for which s1 and s2 are k-similar.

```
func getSwappedStr(arr string, i, j int) string {
    if i < 0 || j < 0 || i >= len(arr) || j >= len(arr) {
        return arr
    }
    // make sure i is always first
    if i > j {
        tmp := i
        i = j
        j = tmp
    }
    // catfood
    // cdtfooa

	return arr[:i] + string(arr[j]) + arr[i+1:j] + string(arr[i]) + arr[j+1:]
}

func getNeighbors(s, b string) []string {
    res := []string{}

    i := 0
    for ; i < len(s); i++ {
        if s[i] != b[i] {
            break
        }
    }
    // i is now marking the first unequal
    for j := i + 1; j < len(s); j++ {
        if s[j] == b[i] {
            sStr := getSwappedStr(s, i, j)
            res = append(res, sStr)
        }
    }
    return res
}

func kSimilarity(s1 string, s2 string) int {
    
    q := []string{}
    visitedSet := make(map[string]bool)
    q = append(q, s1)
    visitedSet[s1] = true
    level := 0

    for len(q) != 0 {
        sz := len(q)
        for i := 0; i < sz; i++ {
            curr := q[0]
            q = q[1:]
            if curr == s2 {
                return level
            }

            for _, neighbor := range getNeighbors(curr, s2) {
                if _, ok := visitedSet[neighbor]; !ok {
                    q = append(q, neighbor)
                    visitedSet[neighbor] = true
                }

            }
        }

        level++
    }
    return -1
}

```

Solution thoughts:
In fact, the essence of the problem is to get the minimum number of swaps A needs to make itself equal to B.

It is a shortest-path problem so we can utilize BFS. The graph we build sets all possible strings that can be swapped from A as nodes, and an edge exists if one string can be transformed into the other by one swap. We start at A, and target at B.

However, that will cause TLE.

We set all possible strings that can be formed by swapping the positions of two letters in A' one time as neighbours of A', however, only those can make A and B differ less are meaningful neighbours. That is, if A'[i] != B[i] but A'[j] == B[i], the string formed by swap(A, i, j) is a meaningful neighbour of A'. Please note that we just need to swap the first pair (A'[i], A'[j]) we meet because the order of swap doesn't matter.