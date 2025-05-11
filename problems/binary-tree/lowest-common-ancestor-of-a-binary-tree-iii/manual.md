### Solution
```go
func depth(node *Node) int {
    result := 0
    for node != nil {
        result += 1
        node = node.Parent
    }
    return result
}

func lowestCommonAncestor(p *Node, q *Node) *Node {
    pDepth := depth(p)
    qDepth := depth(q)
    if qDepth > pDepth {
        p, q = q, p
        pDepth, qDepth = qDepth, pDepth
    }
    for i := 0; i < (pDepth - qDepth); i++ {
        p = p.Parent
    }
    for p != q {
        p = p.Parent
        q = q.Parent
    }
    return p
}
```
### Time
O(N) -- потому что проходим все дерево в худшем случае
### Memory
O(1) -- Потому что не используем доп память для рекурсии
### Explication
Сначала находим глубину каждой вершины. Затем нам надо уровнять их глубины, то есть поднять самую глубокую
вврех. И вот сейчас когда они на одной глубине, мы можем искать их общего ancestor.