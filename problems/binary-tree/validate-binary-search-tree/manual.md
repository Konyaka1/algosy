### Solution
```go
import "math"

func isValidBST(root *TreeNode) bool {
return isValidSubtree(root, math.MinInt64, math.MaxInt64)
}

func isValidSubtree(root *TreeNode, lower, upper int64) bool {
if root == nil {
return true
}
val := int64(root.Val)
if !(lower < val && val < upper) {
return false
}
return isValidSubtree(root.Left, lower, val) && isValidSubtree(root.Right, val, upper)
}
```

### Time
O(N) -- потому что проверяем каждую вершину
### Memory
O(h) -- высота дерева (в худшем случае N, в среднем logN)
### Explication
Проходим по каждой вершине с проверкой ее возможной левой и правой границы.
Важно приводить в int64, иначе проверка когда значение вершины min/max int32 то произойдет ошибка.

Note: import math и math.MinInt64 надо использовать