# Substring with largest variance
- Lc 2272
`
The variance of a string is defined as the largest difference between the number of occurrences of any 2 characters present in the string. Note the two characters may or may not be the same.

Given a string s consisting of lowercase English letters only, return the largest variance possible among all substrings of s.
`

- kadane's alg
- need max func

`
func largestVariance(s string) int {
    result := 0
    chars := make(map[rune]struct{}) 
    for _, c := range s {
        chars[c] = struct{}{}
    }

    for x, _ := range chars {
        for y, _ := range chars {
            if x == y {
                continue
            }
            totalX := 0
            totalY := 0
            for _, c := range s {
               switch c {
                  case x: totalX += 1 
                  case y: totalY += 1
                  default: continue
               } 

               if totalY > 0 {
                   result = max(result, totalX - totalY)
               } else {
                   result = max(result, totalX - 1)
               }

               if totalX - totalY < 0 {
                   totalX = 0
                   totalY = 0
               }
            }
        }
    }
    return result 
}
`