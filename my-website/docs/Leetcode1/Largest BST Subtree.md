333. Given the root of a binary tree, find the largest subtree, which is also a Binary Search Tree (BST), where the largest means subtree has the largest number of nodes.

note it is important to use min, max because we need to make sure its a BST not just a BT
```
func max(x, y int) int {
    if x > y {
        return x
    }
    return y
}

func min(x, y int) int {
    if x < y {
        return x
    }
    return y
}

func largestBSTSubtree(root *TreeNode) int {
    _, _, nodeCount := largestBST(root)
    return nodeCount   
}

// returns min, max, and nodeCount bst in its subtree
func largestBST(treeNode *TreeNode) (int, int, int) {
    if treeNode == nil {
        return math.MaxInt, math.MinInt, 0
    }
    leftMin, leftMax, leftCount := largestBST(treeNode.Left)
    rightMin, rightMax, rightCount := largestBST(treeNode.Right)
    
    // if its inside our valid range
    if treeNode.Val > leftMax && treeNode.Val < rightMin {
        return min(treeNode.Val, leftMin), max(treeNode.Val, rightMax), leftCount + rightCount + 1
    } else {
        // else, keep looking for a bst
        return math.MinInt, math.MaxInt, max(leftCount, rightCount)
    }
}
```