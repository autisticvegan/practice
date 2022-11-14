I:

II:
Given a string s and a dictionary of strings wordDict, add spaces in s to construct a sentence where each word is a valid dictionary word. Return all such possible sentences in any order.

Note that the same word in the dictionary may be reused multiple times in the segmentation.
---

Note difference is that 

Decision tree, sub problems of breaking things up (backtracking)

keep track of index, number of decisions in tree is based on words in dict

i = 0

leet code

i = 4





Golang
```

```

C++
```
    bool wordBreak(string s, vector<string>& vdict) {
        if(vdict.size()==0) return false;

        std::unordered_set<std::string> dict{vdict.begin(), vdict.end()};
        
        int longestWord = 0;
        for(string word : dict){
            longestWord = max(longestWord, (int)word.size());
        }

        vector<bool> dp(s.size()+1,false);
        dp[0]=true;

        for(int i=1;i<=s.size();i++)
        {
            for(int j=i-1;j>=max(i-longestWord, 0);j--)
            {
                if(dp[j])
                {
                    string word = s.substr(j,i-j);
                    if(dict.find(word)!= dict.end())
                    {
                        dp[i]=true;
                        break; //next i
                    }
                }
            }
        }

        return dp[s.size()];
    }
```

lc sol:
The intuition behind this approach is that the given problem (sss) can be divided into subproblems s1s1s1 and s2s2s2. If these subproblems individually satisfy the required conditions, the complete problem, sss also satisfies the same. e.g. "catsanddog\text{catsanddog}catsanddog" can be split into two substrings "catsand\text{catsand}catsand", "dog\text{dog}dog". The subproblem "catsand\text{catsand}catsand" can be further divided into "cats\text{cats}cats","and\text{and}and", which individually are a part of the dictionary making "catsand\text{catsand}catsand" satisfy the condition. Going further backwards, "catsand\text{catsand}catsand", "dog\text{dog}dog" also satisfy the required criteria individually leading to the complete string "catsanddog\text{catsanddog}catsanddog" also to satisfy the criteria.

Now, we'll move onto the process of dp\text{dp}dp array formation. We make use of dp\text{dp}dp array of size n+1n+1n+1, where nnn is the length of the given string. We also use two index pointers iii and jjj, where iii refers to the length of the substring (s′s's′) considered currently starting from the beginning, and jjj refers to the index partitioning the current substring (s′s's′) into smaller substrings s′(0,j)s'(0,j)s′(0,j) and s′(j+1,i)s'(j+1,i)s′(j+1,i). To fill in the dp\text{dp}dp array, we initialize the element dp[0]\text{dp}[0]dp[0] as true\text{true}true, since the null string is always present in the dictionary, and the rest of the elements of dp\text{dp}dp as false\text{false}false. We consider substrings of all possible lengths starting from the beginning by making use of index iii. For every such substring, we partition the string into two further substrings s1′s1's1′ and s2′s2's2′ in all possible ways using the index jjj (Note that the iii now refers to the ending index of s2′s2's2′). Now, to fill in the entry dp[i]\text{dp}[i]dp[i], we check if the dp[j]\text{dp}[j]dp[j] contains true\text{true}true, i.e. if the substring s1′s1's1′ fulfills the required criteria. If so, we further check if s2′s2's2′ is present in the dictionary. If both the strings fulfill the criteria, we make dp[i]\text{dp}[i]dp[i] as true\text{true}true, otherwise as false\text{false}false.