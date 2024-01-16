### [111. 二叉树的最小深度](https://leetcode.cn/problems/minimum-depth-of-binary-tree/description/)

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number}
 */
var minDepth = function(root) {
    if (!root) return 0
    const q = []
    q.push(root)
    let depth = 1

    while (q.length) {
        const size = q.length
        
        for (let i = 0; i < size; i++) {
            const node = q.shift()
            if (!node.left && !node.right) {
                return depth
            }
            if (node.left !== null) {
                q.push(node.left)
            }
            if (node.right !== null) {
                q.push(node.right)
            }
        }
        
        depth++
    }
};
```