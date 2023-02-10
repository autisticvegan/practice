`
You are playing a game that has n levels numbered from 0 to n - 1. You are given a 0-indexed integer array damage where damage[i] is the amount of health you will lose to complete the ith level.

You are also given an integer armor. You may use your armor ability at most once during the game on any level which will protect you from at most armor damage.

You must complete the levels in order and your health must be greater than 0 at all times to beat the game.

Return the minimum health you need to start with to beat the game.
`

`
func minimumHealth(damage []int, armor int) int64 {
    var sumDamage, maxDamage int
    
    for _, d := range damage {
        sumDamage += d
        maxDamage = max(maxDamage, d)
    }
	
    return int64(sumDamage - min(armor, maxDamage) + 1)
}

func max(a, b int) int {
    if a > b {
        return a
    }
    return b
}

func min(a, b int) int {
    if a < b {
        return a
    }
    return b
}
`