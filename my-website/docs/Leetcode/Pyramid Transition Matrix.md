754. Pyramid Trasition Matrix

![problem](/images/754_0.jpg)

```
func pyramidTransition(bottom string, allowed []string) bool {
    nexts := map[string][]byte{}
    for _, v := range allowed {
        nexts[v[:2]] = append(nexts[v[:2]], v[2])
    }

    var dfs func(cur []byte, i int) bool
    dfs = func(cur []byte, i int) bool {
        if len(cur) == 1 {
            return true
        }
        if len(cur) == i+1 {
            return dfs(cur[:len(cur)-1], 0)
        }
        s := string(cur[i : i+2])
        for _, c := range nexts[s] {
            cur[i] = c // no need to backtrack
            if dfs(cur, i+1) {
                return true
            }
        }
        return false
    }

    return dfs([]byte(bottom), 0)
}
```