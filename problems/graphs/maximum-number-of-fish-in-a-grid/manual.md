### Solution
With used
```golang
func findMaxFish(grid [][]int) int {
    max := 0
    for i := range grid {
        for j := range grid[i] {
            res := dfs(i, j, grid)
            if res > max {
                max = res
            }
        }
    }

    return max
}

func dfs(x, y int, grid [][]int) int {
    if ok := canVisit(x, y, grid); !ok {
        return 0
    }

    cur := grid[x][y]
    grid[x][y] = 0

    return cur + dfs(x + 1, y, grid) + dfs(x - 1, y, grid) + dfs(x, y + 1, grid) + dfs(x, y - 1, grid)
}

func canVisit(x, y int, grid [][]int) bool {
    if x < 0 || x >= len(grid) {
        return false
    }
    if y < 0 || y >= len(grid[0]) {
        return false
    }

    if grid[x][y] == 0 {
        return false
    }

    return true
}
```
### Time
O(N * M) -- Потому что проходим по всем элементам массива
### Memory
O(N * M) -- Память для обхода, если все клетки являются 'O'.
### Explication
Пример для того, чтобы лучше понять условие
```text
Совершаем подсчет каждого острова и ищем максимальное значение. После обхода каждую вершину можно 
помечать как ноль, чтобы не использовать массив used.

NOTE: Нужен строгий паттерн решения задач на обходы.

пока вырисовывается такая картина: есть два метода: dfs + canVisit... 
```