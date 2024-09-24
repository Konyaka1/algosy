### Solution

```java
class NumMatrix {

    final int[][] prMatr;

    public NumMatrix(int[][] matrix) {
        int m = matrix.length;
        int n = matrix[0].length;

        this.prMatr = new int[m + 1][n + 1];

        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                this.prMatr[i + 1][j + 1] = matrix[i][j] + this.prMatr[i][j + 1] + this.prMatr[i + 1][j] - this.prMatr[i][j];
            }
        }
    }

    public int sumRegion(int row1, int col1, int row2, int col2) {
        int wholeRegion = this.prMatr[row2 + 1][col2 + 1];
        int leftRegion = this.prMatr[row2 + 1][col1];
        int upRegion = this.prMatr[row1][col2 + 1];
        int intersectionRegion = this.prMatr[row1][col1];

        return wholeRegion - leftRegion - upRegion + intersectionRegion;
    }
}
```
### Time
- creation: O(N * M) -- где N кол-во элементов в одной строке, а M кол-во строк
- sumRegion: O(1) -- сумма/разность 4 чисел
### Memory
- creation: O(N * M) -- где N кол-во элементов, создается массив размером N*M
- sum range: O(1) -- память не нужна
### Explication
Создаем массив размером (N + 1) * (M + 1), и храним префиксные суммы там.
`prMatr[i + 1][j + 1] == matr[i][j] + prMatr[i + 1][j] + prMatr[i][j + 1] - prMatr[i][j]`.
Каждый следующий элемент равен сумме текущего элемента в матрице, плюс предыдущая сумма "сверху", 
плюс предыдущая сумма "слева", минус пересечение этих двух сумм.

Для подсчета региона `x1, y1, x2, y2`, где x,y координаты начинающиеся с нуля, используем формулу:
`sum(x1,y1,x2,y2) = sum(0,0,x2,y2) - sum(0,0,x2,y1-1) - sum(0,0,x1-1,y2) + sum(0,0,x1-1,x2-2)`. то есть мы отнимаем
левый прямоугольник, отнимаем верхний прямоугольник, и прибавляем их пересечение. Таким образом:
`sum(x1,y1,x2,y2) = prMatr(x2 + 1, y2 + 1) - prMatr(x1, y2 + 1) - prMatr(x2 + 1, y1) + prMatr(x1, y1)`

