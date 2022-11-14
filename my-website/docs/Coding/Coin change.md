322. Coin Change

You are given an integer array coins representing coins of different denominations and an integer amount representing a total amount of money.

Return the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return -1.

Think about relationship between {amount, n}

```
class Solution {
public:
    int coinChange(vector<int>& coins, int amount) {
        vector<int>h((amount+1), INT_MAX-1);
        h[0] = 0;
        for(int i = 0; i < h.size(); i++)
        {
            for(int j = 0; j < coins.size(); j++)
            {
                if(i >= coins[j]) h[i] = min(h[i], 1 + h[i-coins[j]]);
            }
        }
        return (h[h.size()-1] < INT_MAX - 1)?h[h.size()-1]:-1; 
    }
};
```