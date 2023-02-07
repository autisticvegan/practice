
- depending on if you want space/time or not - can do a O(n^2) and O(n^2) sol (technically CN^2 where C is the largest number in the set), or a O(1) and O(n^4) sol, or an O(n) and O(n^3) 
- basically pre-compute sums and try to turn it into a diff problem

`
    /**
     * Runtime O(n^2) and Space O(n^2)
     */
    public List<List<Integer>> fourSum(int[] nums, int target) {
        Set<List<Integer>> res = new HashSet<>();
        int len = nums.length;
        
        Map<Integer, Set<List<Integer>>> sum2Nums = new HashMap<>();
        for (int i = 0; i < len - 1; i++) {
            for (int j = i + 1; j < len; j++) {
                sum2Nums.computeIfAbsent(nums[i] + nums[j], k -> new HashSet<>()).add(Arrays.asList(i, j));
            }
        }
        for (int i = 0; i < len - 1; i++) {
            for (int j = i + 1; j < len; j++) {
                int s = target - (nums[i] + nums[j]);
                if (sum2Nums.containsKey(s)) {
                    for (List<Integer> kl : sum2Nums.get(s)) {
                        if (kl.get(0) > j && kl.get(1) > j) {
                            // even with this index arranging, the quardruplet of [i,j,k,l] is never dup, but 
                            // [nums[i], nums[j], nums[k], nums[l]] may still be dup when those 4 nums are
                            // not all different from each other, so use Set<List<Integer>> for result.
                            // Further more, the quardruplet need to follow certain order for the set to
                            // differentiate them, hence need sorting. This sort on 4 elements may not be a big deal
                            List<Integer> quard = Arrays.asList(nums[i], nums[j], nums[kl.get(0)], nums[kl.get(1)]);
                            Collections.sort(quard);
                            res.add(quard);
                        }
                    }
                }
            }
        }
        return new ArrayList<>(res);
    }
`

`
#!/usr/bin/env python3

def pair_sum(array, target):
    H = {}
    for index, value in enumerate(array):
        remainder = target - value
        if remainder in H:
            return (value, array[H[remainder]])
        else:
            H[value] = index
    return None

print(pair_sum([1, 2, 3, 4, 6, 7], 6))

def four_sum(array, target):
    H = {}
    for i in range(len(array) - 1):
        for j in range(i + 1, len(array)):
            pair = array[i] + array[j]
            remainder = target - pair
            if remainder in H:
                a, b = H[remainder]
                if a != i and b != i and a != j and b != j:
                    return (array[a], array[b], array[i], array[j])
            else:
                H[pair] = (i, j)
    return None

print(four_sum([-3, -2, 1, -4, 3, -5, 5, 10, 8, 3, 4], 0))
`

`
def foursum(arr, targ):
    answers = []

    # generate sum of pairs

    pairs=[]
    for i, x in enumerate(arr):
        pairsi = [("x+y", x+y) for y in arr[i+1:]]
        pairs.extend(pairsi)
    
    # foreach sum of pairs, see if you can make targ from another sum of pairs in the list you havent visited yet

    for i, x in enumerate(pairs):
        v=x[1]
        target = targ - v
        for pot in pairs[i+1:]:
            if pot[1] == target:
                ans = sorted(pot[0].split("+") + v.split("+"))
                answers.append(ans)
    
    # deduplicate
    return list(set(answers))
`