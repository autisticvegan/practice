Given an array of strings words and a width maxWidth, format the text such that each line has exactly maxWidth characters and is fully (left and right) justified.

You should pack your words in a greedy approach; that is, pack as many words as you can in each line. Pad extra spaces ' ' when necessary so that each line has exactly maxWidth characters.

Extra spaces between words should be distributed as evenly as possible. If the number of spaces on a line does not divide evenly between words, the empty slots on the left will be assigned more spaces than the slots on the right.

For the last line of text, it should be left-justified, and no extra space is inserted between words.

Note:

    A word is defined as a character sequence consisting of non-space characters only.
    Each word's length is guaranteed to be greater than 0 and not exceed maxWidth.
    The input array words contains at least one word.



```
func nextWords(words []string, maxWidth int, index int) ([]string, int) {
	result := make([]string, 0)

	width := 0
	first := true

	for {
		if index >= len(words) {
			return result, index
		}

		word := words[index]

		width += len(word)
		if !first {
			width++
		} else {
			first = false
		}

		if width > maxWidth {
			return result, index
		}

		result = append(result, word)

		index++
	}
}

func generateRow(words []string, maxWidth int, lastRow bool) string {
	if lastRow {
		result := strings.Join(words, " ")

		return result + strings.Repeat(" ", maxWidth-len(result))
	}

	totalWordsWidth := 0
	for _, word := range words {
		totalWordsWidth += len(word)
	}

	result := ""
	for index, word := range words {
		result += word
		totalWordsWidth -= len(word)
		extraSpace := maxWidth - len(result) - totalWordsWidth
		wordsLeft := len(words) - index - 1

		if wordsLeft == 0 {
			result += strings.Repeat(" ", maxWidth-len(result))
		} else {
			result += strings.Repeat(" ", extraSpace/wordsLeft)
			if extraSpace%wordsLeft != 0 {
				result += " "
			}
		}
	}

	return result
}

func fullJustify(words []string, maxWidth int) []string {
	results := make([]string, 0)

	index := 0

	for {
		var row []string
		row, index = nextWords(words, maxWidth, index)

		results = append(results, generateRow(row, maxWidth, index >= len(words)))

		if index >= len(words) {
			break
		}
	}

	return results
}
```