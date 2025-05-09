### Solution
```go
func sortedArrayToBST(nums []int) *TreeNode {
    return buildTree(nums, 0, len(nums))
}

func buildTree(nums []int, l, r int) *TreeNode {
    if l >= r {
        return nil
    }

    m := (l + r) / 2

    left := buildTree(nums, l, m)
    right := buildTree(nums, m + 1, r)

    return &TreeNode{
        Val: nums[m],
        Left: left,
        Right: right,
    }
}
```
### Time
O(N) -- потому что проходим весь массив
### Memory
O(logN) -- потому что обходим сбалансированное дерево
### Explication
Обходим массив с середины и строим дерево. Так как мы строим с середины, мы знаем что слева и справа
будут равное количество элементов для каждой вершины.