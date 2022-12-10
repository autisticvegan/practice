min camera cover binary tree

```
// 3 states
int NO_CAMERA_AND_NOT_BEING_WATCHED = 0;
int NO_CAMERA_AND_BEING_WATCHED = 1;
int HAS_CAMERA = 2;

class Solution {
public:
    
    // if node is null, then that means it has NO CAMERA yet is being watched (state 1)
    // because the parent has a camera
    int getCameraStatus(TreeNode* node, int* res) {
        if (node == nullptr) {
            return NO_CAMERA_AND_BEING_WATCHED;
        }
        
        // get the left and right states
        int left = getCameraStatus(node->left, res);
        int right = getCameraStatus(node->right, res);
        
        // if the left OR the right is not being watched, add a camera and return 2
        if (left == NO_CAMERA_AND_NOT_BEING_WATCHED || right == NO_CAMERA_AND_NOT_BEING_WATCHED) {
            *res = *res + 1;
            return HAS_CAMERA;
        }
        
        // if the left OR the right HAS a camera, then state 1
        if (left == HAS_CAMERA || right == HAS_CAMERA) {
            return NO_CAMERA_AND_BEING_WATCHED;
        }
        
        // else return state 0
        return NO_CAMERA_AND_NOT_BEING_WATCHED;
    }
    
    int minCameraCover(TreeNode* root) {
 
        int res = 0;
        if (getCameraStatus(root, &res) == 0) {
            ++res;
        }
        
        return res;
    }
};
```
```
package main

// 3 possible states:
// node doesnt have a camera and is not being watched - state 0
//

const (
	NO_CAMERA_AND_NOT_BEING_WATCHED int = 0
	NO_CAMERA_AND_BEING_WATCHED         = 1
	HAS_CAMERA                          = 2
)

func getCameraStatus(node *TreeNode, res *int) int {
	if node == nil {
		return NO_CAMERA_AND_BEING_WATCHED
	}

	left := getCameraStatus(node.Left, res)
	right := getCameraStatus(node.Right, res)

	// if left or right is not being watched, install camera here
	if left == NO_CAMERA_AND_NOT_BEING_WATCHED || right == NO_CAMERA_AND_NOT_BEING_WATCHED {
		*res = *res + 1
		return HAS_CAMERA
	}

	if left == HAS_CAMERA || right == HAS_CAMERA {
		return NO_CAMERA_AND_BEING_WATCHED
	}

	return NO_CAMERA_AND_NOT_BEING_WATCHED
}

func minCameraCover(node *TreeNode) int {
	res := 0

	// need to check for extra camera because root has no parent
	// if left and right are both 1, , but root is 0, then add an extra one
	if getCameraStatus(node, &res) == 0 {
		res++
	}

	return res
}
```