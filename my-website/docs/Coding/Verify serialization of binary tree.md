Verify Preorder Serialization of a Binary Tree

One way to serialize a binary tree is to use preorder traversal. When we encounter a non-null node, we record the node's value. If it is a null node, we record using a sentinel value such as '#'.

For example, the above binary tree can be serialized to the string "9,3,4,#,#,1,#,#,2,#,6,#,#", where '#' represents a null node.

Given a string of comma-separated values preorder, return true if it is a correct preorder traversal serialization of a binary tree.

```
class Solution {
public:
    bool isValidSerialization(string preorder) {
           if (preorder.empty()) return false;
    preorder+=',';
    int sz=preorder.size(),idx=0;
    int capacity=1;
    for (idx=0;idx<sz;idx++){
        if (preorder[idx]!=',') continue;
        capacity--;
        if (capacity<0) return false;
        if (preorder[idx-1]!='#') capacity+=2;
    }
    return capacity==0;
    }
};
```