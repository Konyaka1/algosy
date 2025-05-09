## Fails
### 1st try
Ошибка в логике, неправильный ответ
```go
func isValidBST(root *TreeNode) bool {
    if root == nil {
        return true
    }
    if root.Left == nil && root.Right == nil {
        return true
    }
    if root.Right == nil {
        if root.Left.Val >= root.Val {
            return false
        }
        return isValidBST(root.Left)
    }
    if root.Left == nil {
        if root.Right.Val <= root.Val {
            return false
        }
        return isValidBST(root.Right)
    }
    
    if root.Left.Val >= root.Val || root.Right.Val <= root.Val {
        return false
    }
    
    return isValidBST(root.Left) && isValidBST(root.Right)
}

```
### 2nd try
Ошибка в проверки крайних условий
```go
func isValidBST(root *TreeNode) bool {
    if root == nil {
        return true
    }
    return isValidSubtree(root.Left, -2147483648, root.Val) && isValidSubtree(root.Right, root.Val, 2147483647)
}

func isValidSubtree(root *TreeNode, lower, upper int) bool {
    if root == nil {
        return true
    }
    if !(lower < root.Val && root.Val < upper) {
        return false
    }
    return isValidSubtree(root.Left, lower, root.Val) && isValidSubtree(root.Right, root.Val, upper)
}

```