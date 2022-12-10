Minimum Moves to Make Array Complementary

```
You are given an integer array nums of even length n and an integer limit. In one move, you can replace any integer from nums with another integer between 1 and limit, inclusive.

The array nums is complementary if for all indices i (0-indexed), nums[i] + nums[n - 1 - i] equals the same number. For example, the array [1,2,3,4] is complementary because for all indices i, nums[i] + nums[n - 1 - i] = 5.

Return the minimum number of moves required to make nums complementary.
```

```
For each pair of numbers (at index i and N - 1 - i) l and r:

    By 2 moves we can get any number between [2, limit*2] (including move a number to the same number)
    After only one move (change one of the numbers to a number between 1 and limit)
        The minimum sum we can get is (min(l, r) + 1) (let this be oneMoveMin)
        The maximum sum we can get is (max(l, r) + limit) (let this be oneMoveMax)
    We need no move to get (l + r) (let this be justGood)

Therefore, to get:

    [~, oneMoveMin - 1] - 2 moves
    [oneMoveMin, justGood-1] - 1 move
    [justGood] - 0 move
    [justGood + 1, oneMoveMax] - 1 move
    [oneMoveMax + 1, ~] - 2 moves

For each pair of numbers

    We start with 2 moves
    From oneMoveMin we need 1 less move
    From justGood we need another 1 less move
    From justGood + 1 we need 1 more move
    From oneMoveMax + 1 we need another 1 more move

For all numbers

    We can at most move N times
    From 2 to limit*2, we accumulate the number of moves all pairs of numbers subtract/add
    Find the smallest

```


```
We know that optimal sum would lie between [2, 2*limit]
We are basically trying to calculate for each sum how many numbers need to be changed.
To do that we look at each pair (l,r) and divide it into regions where we need 2,1,0,1,2 moves as explained earlier in the post by author.
Based on this we can make a difference array to mark these critical points where the moves actually change.
And then we can traverse this difference array to get actual number of moves for that particular sum.
```

```
int minMoves(vector<int>& nums, int limit) {
    int N = nums.size();
    vector<int> memo(limit*2 + 2, 0);
    for (int i = 0; i < N/2; ++i) {
        int l = nums[i], r = nums[N-1-i];
        --memo[min(l, r) + 1];
        --memo[l + r];
        ++memo[l + r + 1];
        ++memo[max(l, r) + limit + 1];
    }
    int ans = N, curr = N;
    for (int i = 2; i <= limit*2; ++i) {
        curr += memo[i];
        ans = min(ans, curr);
    }
    return ans;
}
```