## Reorder Data in Log Files (937)
1. Separate the letter logs from the number logs
2. Sort the letter logs, first on log content, then on identifier
3. Append the number logs to the letter logs

`
You are given an array of logs. Each log is a space-delimited string of words, where the first word is the identifier.

There are two types of logs:

    Letter-logs: All words (except the identifier) consist of lowercase English letters.
    Digit-logs: All words (except the identifier) consist of digits.

Reorder these logs so that:

    The letter-logs come before all digit-logs.
    The letter-logs are sorted lexicographically by their contents. If their contents are the same, then sort them lexicographically by their identifiers.
    The digit-logs maintain their relative ordering.

Return the final order of the logs.
`

`
func reorderLogFiles(logs []string) []string {
    if len(logs) < 2 {
        return logs
    }
    
    var sortedStrLogs []string
    var sortedNumLogs []string
    for _, log := range logs {
        i := strings.Index(log, " ")
        if log[i+1] >= 'a' && log[i+1] <= 'z' {
            sortedStrLogs = append(sortedStrLogs, log)
        } else {
            sortedNumLogs = append(sortedNumLogs, log)
        }
    }
    
    sort.Slice(sortedStrLogs, func (i, j int) bool {
        iIndex := strings.Index(sortedStrLogs[i], " ")
        jIndex := strings.Index(sortedStrLogs[j], " ")
        
        iLog := sortedStrLogs[i][iIndex+1:]
        jLog := sortedStrLogs[j][jIndex+1:]
        if iLog == jLog {
            return sortedStrLogs[i] < sortedStrLogs[j]
        }
        return iLog < jLog
    })
    
    sortedStrLogs = append(sortedStrLogs, sortedNumLogs...)
    return sortedStrLogs
}
`