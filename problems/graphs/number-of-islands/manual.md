### Solution
With modification of input
```java
class Solution {
    public int numIslands(char[][] grid) {
        int m = grid.length;
        int n = grid[0].length;

        Deque<int[]> deq = new ArrayDeque<>();

        int result = 0;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] == '0') {
                    continue;
                }
                deq.offerLast(new int[]{i, j});
                this.bfs(deq, grid);

                result = result + 1;
            }
        }

        return result;
    }

    private void bfs(Deque<int[]> deq, char[][] grid) {
        while (!deq.isEmpty()) {
            int[] coord = deq.pollFirst();
            int x = coord[0];
            int y = coord[1];

            if (x < 0 || x >= grid.length) {
                continue;
            }
            if (y < 0 || y >= grid[0].length) {
                continue;
            }

            if (grid[x][y] == '0') {
                continue;
            }

            grid[x][y] = '0';

            deq.offerLast(new int[]{x + 1, y});
            deq.offerLast(new int[]{x, y + 1});
            deq.offerLast(new int[]{x - 1, y});
            deq.offerLast(new int[]{x, y - 1});
        }
    }

    private void dfs(Deque<int[]> deq, char[][] grid) {
        while (!deq.isEmpty()) {
            int[] coord = deq.pollLast();
            int x = coord[0];
            int y = coord[1];

            if (x < 0 || x >= grid.length) {
                continue;
            }
            if (y < 0 || y >= grid[0].length) {
                continue;
            }

            if (grid[x][y] == '0') {
                continue;
            }
            grid[x][y] = '0';

            deq.offerLast(new int[]{x + 1, y});
            deq.offerLast(new int[]{x, y + 1});
            deq.offerLast(new int[]{x - 1, y});
            deq.offerLast(new int[]{x, y - 1});
        }
    }
}
```
No input modification
```java
class Solution {
    public int numIslands(char[][] grid) {
        int m = grid.length;
        int n = grid[0].length;
        boolean[][] used = new boolean[m][n];
        
        Deque<int[]> deq = new ArrayDeque<>();
        
        int result = 0;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (used[i][j] || grid[i][j] == '0') {
                    continue;
                }
                deq.offerLast(new int[]{i, j});
                this.dfs(deq, used, grid, n, m);
                
                result = result + 1;
            }
        }
        
        return result;
    }
    
    private void dfs(Deque<int[]> deq, boolean[][] used, char[][] grid, int n, int m) {
        while (!deq.isEmpty()) {
            int[] coord = deq.pollLast();
            int x = coord[0];
            int y = coord[1];
            
            if (x < 0 || x >= m) {
                continue;
            }
            if (y < 0 || y >= n) {
                continue;
            }
            
            if (used[x][y] || grid[x][y] == '0') {
                continue;
            }
            
            used[x][y] = true;
            
            deq.offerLast(new int[]{x + 1, y});
            deq.offerLast(new int[]{x, y + 1});
            deq.offerLast(new int[]{x - 1, y});
            deq.offerLast(new int[]{x, y - 1});     
        }
    }
}
```
### Time
O(N * M) -- Потому что проходим по всем элементам массива
### Memory
O(N * M) -- Храним матрицу такого же размера для отметки пройденных частей, или для хранения всей очереди если 
все является одним островом.
### Explication
* Для решения задачи используем bfs или dfs. Идея в том, чтобы найти точку "земли". Как только мы ее нашли, 
запускаем dfs/bfs. В dfs/bfs мы помечаем все точки земли как пройденные. Как только мы закончили обход,
прибавляем единицу к количеству островов. Делаем это в цикле по каждой точке массива. Как только мы нашли
следующую "землю", которую мы еще не обходили, опять запускаем dfs/bfs. Таким образом мы пройдем по всем точкам массива
и найдем все острова. Кратко: если точка является землей и она "новая" (мы еще не обходили ее), то добавляем 1 к ответу
и запускаем bfs/dfs и помечаем все клетки острова как пройденные.
* Для решения, когда можно менять входной массив, мы проходим по всем точкам, и если точка не вода -- начинаем обход.
Во время обхода мы "топим" остров, то есть помечаем все клетки острова водой. Закончив обход, прибавляем 1 к ответу.
Повторяем все действия, пока не пройдем все точки матрицы.
