## Fails
### 1st try
Неудачная попытка в замыкание рекурсивное
```go
func kthSmallest(root *TreeNode, k int) int {
    var res int

    func visit(root *TreeNode) {
        if root == nil {
            return
        }
        visit(root.Left)
        i++
        if i == k {
            res = root.Val
            return
        }
    
        
        visit(root.Right)
    }(root)

    return res
}

```
### 2nd try
Forgot to check empty case