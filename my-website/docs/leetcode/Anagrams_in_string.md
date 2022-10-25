Given two strings s and p, return an array of all the start indices of p's anagrams in s. You may return the answer in any order.

An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

 

Example 1:
```
Input: s = "cbaebabacd", p = "abc"
Output: [0,6]
Explanation:
The substring with start index = 0 is "cba", which is an anagram of "abc".
The substring with start index = 6 is "bac", which is an anagram of "abc".
```
Example 2:
```
Input: s = "abab", p = "ab"
Output: [0,1,2]
Explanation:
The substring with start index = 0 is "ab", which is an anagram of "ab".
The substring with start index = 1 is "ba", which is an anagram of "ab".
The substring with start index = 2 is "ab", which is an anagram of "ab".
```

Golang
```
func equal(s, p []int) bool {
    for i := 0; i < len(s); i++ {
        if s[i] != p[i] {
            return false
        }
    }
    return true
}

func findAnagrams(s string, p string) []int {
    res := []int{}

    pVec := make([]int, 26)
    sVec := make([]int, 26)

    if len(s) < len(p) {
        return res
    }

    for i := 0; i < len(p); i++ {
        pVec[p[i] - 97]++
        sVec[s[i] - 97]++
    }

    if equal(sVec, pVec) {
        res = append(res, 0)
    }

    for i := len(p); i < len(s); i++ {

        sVec[s[i] - 97]++
        sVec[s[i - len(p)] - 97]--
        if equal(sVec, pVec) {
            res = append(res, i - len(p) + 1)
        }
    }
    return res
}
```





C++
```
 vector<int> findAnagrams(string s, string p) {
        vector<int> pv(26,0), sv(26,0), res;
        if(s.size() < p.size())
           return res;
        // fill pv, vector of counters for pattern string and sv, vector of counters for the sliding window
        for(int i = 0; i < p.size(); ++i)
        {
            ++pv[p[i]-'a'];
            ++sv[s[i]-'a'];
        }
        if(pv == sv)
           res.push_back(0);

        //here window is moving from left to right across the string. 
        //window size is p.size(), so s.size()-p.size() moves are made 
        for(int i = p.size(); i < s.size(); ++i) 
        {
             // window extends one step to the right. counter for s[i] is incremented 
            ++sv[s[i]-'a'];
            
            // since we added one element to the right, 
            // one element to the left should be discarded. 
            //counter for s[i-p.size()] is decremented
            --sv[s[i-p.size()]-'a']; 

            // if after move to the right the anagram can be composed, 
            // add new position of window's left point to the result 
            if(pv == sv)  // this comparison takes O(26), i.e O(1), since both vectors are of fixed size 26. Total complexity O(n)*O(1) = O(n)
               res.push_back(i-p.size()+1);
        }
        return res;
    }
```