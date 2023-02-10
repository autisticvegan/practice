`
You are given two string arrays username and website and an integer array timestamp. All the given arrays are of the same length and the tuple [username[i], website[i], timestamp[i]] indicates that the user username[i] visited the website website[i] at time timestamp[i].

A pattern is a list of three websites (not necessarily distinct).

    For example, ["home", "away", "love"], ["leetcode", "love", "leetcode"], and ["luffy", "luffy", "luffy"] are all patterns.

The score of a pattern is the number of users that visited all the websites in the pattern in the same order they appeared in the pattern.

    For example, if the pattern is ["home", "away", "love"], the score is the number of users x such that x visited "home" then visited "away" and visited "love" after that.
    Similarly, if the pattern is ["leetcode", "love", "leetcode"], the score is the number of users x such that x visited "leetcode" then visited "love" and visited "leetcode" one more time after that.
    Also, if the pattern is ["luffy", "luffy", "luffy"], the score is the number of users x such that x visited "luffy" three different times at different timestamps.

Return the pattern with the largest score. If there is more than one pattern with the same largest score, return the lexicographically smallest such pattern.
`

`
Intuition

Finding the most popular visit pattern requires going through all of them. Time complexity to generate all of the patterns is O((N3))=O(N!3!(N−3)!)=O(N3)O(\binom{N}{3}) = O(\frac{N!}{3!(N-3)!}) = O(N^3)O((3N​))=O(3!(N−3)!N!​)=O(N3), where nnn - number of websites. We also need to calculate number of users having each of these patterns, so performance would be reduced even further. One can think this is the wrong path, but fortunately, we have the following restriction 3 <= username.length <= 50 confirming that we are on the right path.
Approach

Use brute force approach, while trying to reduce number of patterns to consider.

    As order of visits is important ensure that inputs are all sorted by timestamp.
    Group website visits by users to make couting a bit easier.
    Based on websites visited by particular user generate possible pattern, but instead of precomputing them and then processing, generate one and process it right away to reduce space complexity.
    Count number of users with such pattern.

Complexity

    Time complexity:
        Preparations step takes O(logN)O(log N)O(logN), where NNN is number of website visits.
        Counting number of visits takes O(N)O(N)O(N). This step can be improved by utilizing map and a sorted slice of timestamps.
        Going through all of the patterns O((N3))=O(N!3!(N−3)!)=O(N3)O(\binom{N}{3}) = O(\frac{N!}{3!(N-3)!}) = O(N^3)O((3N​))=O(3!(N−3)!N!​)=O(N3)
        Total complexity is O(N4)O(N^4)O(N4)

    Space complexity:
        As we are processing patterns right away and only group website visits by users, space complexity is O(N)O(N)O(N)

`


`
func mostVisitedPattern(username []string, timestamp []int, website []string) []string {
    // ensure that all of the visits are sorted by timestamp
    sort.Sort(ByTimestamp{
        Username: username,
        Timestamp: timestamp,
        Website: website,
    })
    websitesByUsers := groupWebsitesByUsers(username, timestamp, website)

    var mostVisitedPattern []string
    var bestNumberOfVisits int

    for i, userWebsites := range websitesByUsers {
        // even if all of the users after i have 
        // pattern we won't be able to improve our current best result
        if len(websitesByUsers) - i < bestNumberOfVisits {
                continue
        }
        // go over all possible patterns for i-th user
        generatePatterns(userWebsites, func(pattern []string) {
            numberOfVisits := 0
            // there is no need to check users before i, as we've already 
            // processed their visit patterns
            for _, userWebsites := range websitesByUsers[i:] {
                if containsPattern(userWebsites, pattern) {
                    numberOfVisits++
                }
            }

            // ensure we have lexicographically smallest pattern
            if numberOfVisits > 0 && numberOfVisits == bestNumberOfVisits &&
                comparePatters(pattern, mostVisitedPattern) < 0 {
                
                mostVisitedPattern = pattern
            }

            if numberOfVisits > bestNumberOfVisits {
                bestNumberOfVisits = numberOfVisits
                mostVisitedPattern = pattern
            }
        })
    }
    
    return mostVisitedPattern
}

type ByTimestamp struct {
    Username []string
    Timestamp []int
    Website []string
}

func (s ByTimestamp) Len() int {
    return len(s.Username)
}

func (s ByTimestamp) Swap(i, j int) {
    s.Username[i], s.Username[j] = s.Username[j], s.Username[i]
    s.Timestamp[i], s.Timestamp[j] = s.Timestamp[j], s.Timestamp[i]
    s.Website[i], s.Website[j] = s.Website[j], s.Website[i]
}

func (s ByTimestamp) Less(i, j int) bool {
    return s.Timestamp[i] < s.Timestamp[j]
}

func generatePatterns(websites []string, processPattern func(p []string)) {
    for i := 0; i < len(websites); i++ {
        for j := i+1; j < len(websites); j++ {
            for k := j+1; k < len(websites); k++ {
                processPattern([]string{websites[i], websites[j], websites[k]})
            }
        }
    }
}

func comparePatters(a, b []string) int {
    for i := range a {
        if a[i] < b[i] {
            return -1
        }

        if a[i] > b[i] {
            return 1
        }
    }

    return 0
}

func groupWebsitesByUsers(username []string, timestamp []int, website []string) ([][]string) {
    usernamesToIndex := mapUsernamesToIndex(username)
    visits := make([][]string, len(usernamesToIndex))
    for i := range website {
        userI := usernamesToIndex[username[i]]
        visits[userI] = append(visits[userI], website[i])
    }

    return visits
}

// containsPattern - returns true if specified pattern is
// in the websites. We can improve performance from O(n) by 
// maintaing mapping of websites to timestamps to faster check if 
// specified website was visited after the timestamp
func containsPattern(websites, pattern []string) bool {
    patternI := 0
    for _, w := range websites {
            if w == pattern[patternI] {
                patternI++
                if patternI >= len(pattern) {
                    return true
                }
            }
    }

    return false
}



func mapUsernamesToIndex(username []string) (map[string]int) {
    usersToIndex := map[string]int{}
    i := 0
    for _, user := range username {
        _, ok := usersToIndex[user]
        if ok {
            continue
        }

        usersToIndex[user] = i
        i++
    }

    return usersToIndex
}
`