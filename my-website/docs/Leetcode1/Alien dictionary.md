Alien dictionary

There is a new alien language that uses the English alphabet. However, the order among the letters is unknown to you.

You are given a list of strings words from the alien language's dictionary, where the strings in words are sorted lexicographically by the rules of this new language.

Return a string of the unique letters in the new alien language sorted in lexicographically increasing order by the new language's rules. If there is no solution, return "". If there are multiple solutions, return any of them.

A string s is lexicographically smaller than a string t if at the first letter where they differ, the letter in s comes before the letter in t in the alien language. If the first min(s.length, t.length) letters are the same, then s is smaller if and only if s.length < t.length.

```
Input: words = ["wrt","wrf","er","ett","rftt"]
Output: "wertf"

Input: words = ["z","x"]
Output: "zx"

Input: words = ["z","x","z"]
Output: ""
Explanation: The order is invalid, so return "".

```



```
//1. Build graph using adjacency list
//2. Topological sort:indegree + bfs
func alienOrder(words []string) string {
	charGraph, inDegree := buildGraph(words)
	finalList := topoSort(charGraph, inDegree)
	if len(finalList) == len(inDegree) {
		return strings.Join(finalList, "")
	} else {
		return ""
	}
}
func topoSort(charGraph map[string][]string, inDegree map[string]int) []string {
	keyExist, keyList := findKey(inDegree, 0)
	finalList := []string{}
	for keyExist {
		fmt.Println(keyList)
		finalList = append(finalList, keyList...)
		for _, key := range keyList {
			for _, dKey := range charGraph[key] {
				inDegree[dKey]--
			}
			inDegree[key]--
		}
		keyExist, keyList = findKey(inDegree, 0)
	}
	return finalList
}
func findKey(m map[string]int, value int) (bool, []string) {
	keys := []string{}
	keyExist := false
	for k, v := range m {
		if v == value {
			keys = append(keys, k)
			keyExist = true
		}
	}
	return keyExist, keys
}
func buildGraph(words []string) (map[string][]string, map[string]int) {
	wOrder := make(map[string][]string)
	vIndegree := make(map[string]int)
	for i := 0; i < len(words); i++ {
		word := words[i]
		for j := 0; j < len(word); j++ {
			wOrder[string(word[j])] = []string{}
			vIndegree[string(word[j])] = 0
		}
	}

	for i := 1; i < len(words); i++ {
		word1 := words[i-1]
		word2 := words[i]

		if strings.HasPrefix(word1, word2) && len(word1) > len(word2) {
			fmt.Print("true")
			return nil, nil
		}
		for j := 0; j < len(word1) && j < len(word1); j++ {
			if word1[j] != word2[j] {
				initOrder := []string{}
				prevOrder, ok := wOrder[string(word1[j])]
				if ok {
					for _, c := range prevOrder {
						initOrder = append(initOrder, c)
					}
				}
				initOrder = append(initOrder, string(word2[j]))
				wOrder[string(word1[j])] = initOrder
				vIndegree[string(word2[j])]++
				break
			}
		}
	}
	return wOrder, vIndegree
}
```