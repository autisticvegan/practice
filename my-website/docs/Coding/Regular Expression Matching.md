Given an input string s and a pattern p, implement regular expression matching with support for '.' and '*' where:

    '.' Matches any single character.​​​​
    '*' Matches zero or more of the preceding element.

The matching should cover the entire input string (not partial).

```
func isMatch(s string, p string) bool {
	slen, plen := len(s), len(p)
	var dp [][]bool
	var t []bool
	for i := 0; i <= slen; i++ {
		t = make([]bool, plen+1)
		dp = append(dp, t)
	}

	// dp[i][j] holds a flag that whether s[0:i] mathes to p[0:j].
	// (Note that we take the 0th index as "empty" string case)
	for i := 0; i <= slen; i++ {
		for j := 0; j <= plen; j++ {
			if i == 0 && j == 0 {
				// in case both s and p are empty
				dp[i][j] = true
				continue
			} else if i == 0 {
				// in case only s is empty.
				// To match an empty string, p should be like a*, a*b*, a*.*a*, ....
				// (* should appear in all odd indexes of p)
				dp[i][j] = ((j-1)%2 == 1 && p[j-1] == '*' && dp[i][j-2])
				continue
			} else if j == 0 {
				// in case only p is mepty.
				// No string s cannot match to empty regular expression
				// unless s itself is empty too (which is already handled)
				dp[i][j] = false
				continue
			}

			// in case both s and p are non-empty
			// consider what should be sufficed to be able to say s[i-1] matches to p[j-1]
			// (= dp[i][j] is true).
			if p[j-1] != '*' {
				// if p[j-1] is not '*', then
				// 1) p[j-1] and s[j-1] should match (same character or p[j-1] == '.')
				// 2) p[0:j-1] should match to s[0:i-1]
				dp[i][j] = (p[j-1] == s[i-1] || p[j-1] == '.') && dp[i-1][j-1]
			} else {
				// if p[j-1] is '*', we need to consider two scenarios
				// case1) consume the '*'
				// to consume * and have s[:i] match to p[:j],
				// p[j-2] should equal to s[i-1] (or p[j-2] can be '.' to be equal to any s[i-1])
				// AND s[:i-1] should match to p[:j] as well.
				//                 ↓ i-1
				// s: [ ] [ ] [a] [a]
				// p: [ ] [a] [*] [ ]
				//             ↑ j-1
				//
				//                 ↓ i-1
				// s: [ ] [ ] [b] [a]
				// p: [ ] [.] [*] [ ]
				//             ↑ j-1
				// in other words, because '*' is used with its previous character,
				// for s[i-1] to be included as "a*" or ".*" in p,
				// s[i-2] should also be included in "a*" or ".*".
				if p[j-2] == '.' || p[j-2] == s[i-1] {
					dp[i][j] = dp[i-1][j]
				}
				// case2) skip the '*'
				//                 ↓ i-1
				// s: [ ] [ ] [b] [a]
				// p: [a] [b] [*] [ ]
				//     ↑ j-3   ↑ j-1
				// even if we can't fulfill the condition above, if s[:i-1] matches to p[j-3],
				// we can say s[:i-1] also matches to p[j-1]
				// because '*' can mean "zero" appearance of the previous character.
				// in other words, we can just skip "b*", not using it.
				if dp[i][j-2] == true {
					dp[i][j] = true
				}
			}
		}
	}
	return dp[slen][plen]
```

Short recursive version

```
func isMatch(s string, p string) bool {
    if len(p) == 0 {
        return len(s) == 0
    } else if p[len(p)-1] == '*' {
        return isMatch(s, p[:len(p)-2]) || len(s) > 0 && (p[len(p)-2] == '.' || s[len(s)-1] == p[len(p)-2]) && isMatch(s[:len(s)-1], p)
    } else if len(s) > 0 && (p[len(p)-1] == '.' || s[len(s)-1] == p[len(p)-1]) {
        return isMatch(s[:len(s)-1], p[:len(p)-1])
    }
    return false
}
```