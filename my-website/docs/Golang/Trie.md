
```
type TrieNode struct {
	nodes [26]*TrieNode
	wordEnds int
}

type Trie struct {
	root *TrieNode
}

func (t *Trie) Insert(word string) {
	
	if word == "" {
		return
	}
	
	curr := t.root

	for _, x := range word {
		letterToInsertIndex := x - 'a'
		if curr.nodes[letterToInsertIndex] == nil {
			curr.nodes[letterToInsertIndex] = &TrieNode{}
		} 
		curr = curr.nodes[letterToInsertIndex]
	}

	curr.wordEnds++
}

// count how many words have this prefixes exist already of this word's letters
// i.e. "back" is in Trie, look up "backyard", answer is 1
// Note this works best if incoming words are sorted by length
func (t *Trie) CountPrefix(word string) int {

}

// This problem is for the HRT codesignal question that uses Tries
func (t *Trie) CountPrefixAndInsertAtSameTime(word string) int {
// basically insert, and on each insnertion, count up wordEnds
}

func (t *Trie) Exists(word string) bool {

	curr := t.root

	for _, x := range word {
		index := x - 'a'
		if curr.nodes[index] == nil {
			return false
		}
		curr = curr.nodes[index]
	}
	
	return curr.wordEnds > 0
}

```

