Given the root of a binary tree and an integer targetSum, return all root-to-leaf paths where the sum of the node values in the path equals targetSum. Each path should be returned as a list of the node values, not node references.

```
func pathSum(root *TreeNode, sum int) [][]int {
    var res [][]int
    if root == nil {
        return res
    }
    if root.Left == nil && root.Right == nil {
        if sum == root.Val {
            return append(res, []int{ root.Val })
        }
        return res
    }
    
    for _, path := range pathSum(root.Left, sum - root.Val) {
        res = append(res, append([]int{ root.Val}, path... ))
    }
    for _, path := range pathSum(root.Right, sum - root.Val) {
        res = append(res, append([]int{ root.Val}, path... ))
    }
    return res
}
```