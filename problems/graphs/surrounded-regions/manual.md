### Solution
With used
```java
class Solution {
    public void solve(char[][] board) {
        int x = board.length;
        int y = board[0].length;

        boolean[][] used = new boolean[x][y];

        Deque<int[]> deq = new ArrayDeque<>();

        for (int i = 0; i < x; i++) {
            if (board[i][0] == 'O') {
                deq.offerLast(new int[]{i, 0});
            }
            if (board[i][y - 1] == 'O') {
                deq.offerLast(new int[]{i, y - 1});
            }
        }
        for (int j = 1; j < y - 1; j++) {
            if (board[0][j] == 'O') {
                deq.offerLast(new int[]{0, j});
            }
            if (board[x - 1][j] == 'O') {
                deq.offerLast(new int[]{x - 1, j});
            }
        }

        this.populate(board, used, deq);

        for (int i = 1; i < x - 1; i++) {
            for (int j = 1; j < y - 1; j++) {
                if (board[i][j] == 'O' && !used[i][j]) {
                    board[i][j] = 'X';
                }
            }
        }
    }

    private void populate(char[][] board, boolean[][] used, Deque<int[]> deq) {
        this.bfs(board, used, deq);
    }

    private void dfs(char[][] board, boolean[][] used, Deque<int[]> deq) {
        while (!deq.isEmpty()) {
            int[] coord = deq.pollLast();
            int x = coord[0];
            int y = coord[1];

            if (x < 0 || x >= board.length) {
                continue;
            }
            if (y < 0 || y >= board[0].length) {
                continue;
            }
            if (board[x][y] == 'X' || used[x][y]) {
                continue;
            }

            used[x][y] = true;

            deq.offerLast(new int[] {x + 1, y});
            deq.offerLast(new int[] {x, y + 1});
            deq.offerLast(new int[] {x - 1, y});
            deq.offerLast(new int[] {x, y - 1});
        }
    }

    private void bfs(char[][] board, boolean[][] used, Deque<int[]> deq) {
        while (!deq.isEmpty()) {
            int[] coord = deq.pollFirst();
            int x = coord[0];
            int y = coord[1];

            if (x < 0 || x >= board.length) {
                continue;
            }
            if (y < 0 || y >= board[0].length) {
                continue;
            }
            if (board[x][y] == 'X' || used[x][y]) {
                continue;
            }

            used[x][y] = true;

            deq.offerLast(new int[] {x + 1, y});
            deq.offerLast(new int[] {x, y + 1});
            deq.offerLast(new int[] {x - 1, y});
            deq.offerLast(new int[] {x, y - 1});
        }
    }
}
```
Without using used array
```java
class Solution {
    public void solve(char[][] board) {
        int x = board.length;
        int y = board[0].length;

        Deque<int[]> deq = new ArrayDeque<>();

        for (int i = 0; i < x; i++) {
            if (board[i][0] == 'O') {
                deq.offerLast(new int[]{i, 0});
            }
            if (board[i][y - 1] == 'O') {
                deq.offerLast(new int[]{i, y - 1});
            }
        }
        for (int j = 1; j < y - 1; j++) {
            if (board[0][j] == 'O') {
                deq.offerLast(new int[]{0, j});
            }
            if (board[x - 1][j] == 'O') {
                deq.offerLast(new int[]{x - 1, j});
            }
        }

        this.populate(board, deq);

        for (int i = 0; i < x; i++) {
            for (int j = 0; j < y; j++) {
                if (board[i][j] == 'O') {
                    board[i][j] = 'X';
                    continue;
                }
                if (board[i][j] == '*') {
                    board[i][j] = 'O';
                }
            }
        }
    }

    private void populate(char[][] board, Deque<int[]> deq) {
        this.bfs(board, deq);
    }

    private void dfs(char[][] board, Deque<int[]> deq) {
        while (!deq.isEmpty()) {
            int[] coord = deq.pollLast();
            int x = coord[0];
            int y = coord[1];

            if (x < 0 || x >= board.length) {
                continue;
            }
            if (y < 0 || y >= board[0].length) {
                continue;
            }
            if (board[x][y] == 'X' || board[x][y] == '*') {
                continue;
            }

            board[x][y] = '*';

            deq.offerLast(new int[] {x + 1, y});
            deq.offerLast(new int[] {x, y + 1});
            deq.offerLast(new int[] {x - 1, y});
            deq.offerLast(new int[] {x, y - 1});
        }
    }

    private void bfs(char[][] board, Deque<int[]> deq) {
        while (!deq.isEmpty()) {
            int[] coord = deq.pollFirst();
            int x = coord[0];
            int y = coord[1];

            if (x < 0 || x >= board.length) {
                continue;
            }
            if (y < 0 || y >= board[0].length) {
                continue;
            }
            if (board[x][y] == 'X' || board[x][y] == '*') {
                continue;
            }

            board[x][y] = '*';

            deq.offerLast(new int[] {x + 1, y});
            deq.offerLast(new int[] {x, y + 1});
            deq.offerLast(new int[] {x - 1, y});
            deq.offerLast(new int[] {x, y - 1});
        }
    }
}
```
### Time
O(N * M) -- Потому что проходим по всем элементам массива
### Memory
O(N * M) -- Память для обхода, если все клетки являются 'O'.
### Explication
Пример для того, чтобы лучше понять условие
```text
input=
 [
 ["O","X","X","O","X"],
 ["X","O","O","X","O"],
 ["X","O","X","O","X"],
 ["O","X","O","O","O"],
 ["X","X","O","X","O"]
 ]

 expect =
 [
 ["O","X","X","O","X"],
 ["X","X","X","X","O"],
 ["X","X","X","O","X"],
 ["O","X","O","O","O"],
 ["X","X","O","X","O"]
 ]
```
В этой задаче нужно все 'O' не имеющие контакта с 'O' на границе, пометить как
'X'. 
* Для этого проходим по границам массива и добавляем в очередь все 'O'.
Далее начинаем проход bfs/dfs, чтобы пометить пройденными все 'O' имеющие контакт с границей.
Далее запускам проход в цикле по всем клеткам кроме граничных. Если мы встретили 'O' и эта клетка
не посещена -- перекрашиваем ее в 'X'.
* Второй вариант не подразумевает использование used[][]. Вместо этого все 'O' имеющие контакт с границей
перекрашиваются в '\*' (или любой другой символ). Затем запускается цикл по всем элементам массива.
При нахождении 'O' -- перекрашиваем в 'X'. При нахождении '\*' -- перекрашиваем обратно в 'O'.