### Solution
```go
func kthSmallest(root *TreeNode, k int) int {
    node := visit(root, &k)
    
    return node.Val
}

func visit(root *TreeNode, k *int) *TreeNode {
    if root == nil {
        return nil
    }
    res := visit(root.Left, k)
    if res != nil {
        return res
    }
    *k -= 1
    if *k == 0 {
        return root
    }

    return visit(root.Right, k)
}
```

### Time
O(N) -- потому что проходим в худшем случае все вершины
### Memory
O(H) -- потому что нужна память для рекурсивных вызовов, и все зависит от высоты дерева
### Explication
Проходим по каждой вершине left-in-order traversal. Так мы проходим деревод в порядке возрастания вершин.
В каждом посещении уменьнаем k на 1 и проверяем, может уже дошли до нужной. 

Важно результатом траверсинга сделать саму вершину, а не ее значение. Так можно спокойно проверять на nil
эту вершину, что дает больше возможностей для модификации алгоритма.