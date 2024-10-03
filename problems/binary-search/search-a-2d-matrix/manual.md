### Solution
Left based. Last вхождение
```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        int lengthOfRow = matrix[0].length;

        int lIndex = 0;
        int rIndex = matrix.length * lengthOfRow;

        while (rIndex - lIndex > 1) {
            int m = (rIndex + lIndex) / 2;

            int mi = m / lengthOfRow;
            int mj = m % lengthOfRow;
            if (matrix[mi][mj] <= target) {
                // move l
                lIndex = m;
            } else {
                // move r
                rIndex = m;
            }
        }
        int li = lIndex / lengthOfRow;
        int lj = lIndex % lengthOfRow;

        return target == matrix[li][lj];
    }
}
```
Еще одна идея -- поиск строки и колонки
```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        int row = this.binSearchRow(matrix, target);
        int column = this.binSearchColumn(matrix, target, row);

        return matrix[row][column] == target;
    }

    private int binSearchRow(int[][] matrix, int target) {
        int l = 0;
        int r = matrix.length;

        while (r - l > 1) {
            int m = (r + l) / 2;

            if (matrix[m][0] <= target) {
                l = m;
            } else {
                r = m;
            }
        }

        return l;
    }

    private int binSearchColumn(int[][] matrix, int target, int row) {
        int l = 0;
        int r = matrix[row].length;

        while (r - l > 1) {
            int m = (r + l) / 2;

            if (matrix[row][m] <= target) {
                l = m;
            } else {
                r = m;
            }
        }

        return l;
    }
}
```
### Time
O(log N * M) -- каждый раз мы делим на два, и кол-во операций уменьшается в двое
### Memory
O(1) -- нет нужды в доп памяти зависящей от длины массива
### Explication
Делаем из 2D массива 1D (plain) массив, для этого пользуемся формулой
```text
plain to 2d:
i = plain_index / row_length; Индекс строки
j = plain_index % row_length; Индекс колонки

2d to plain:
plain_index =  (i * row_length) + j, где i -- индекс строки, j -- индекс колонки; оба zero-based.

Example:
2d to plain:  [x00, x01, x02, x03, x10, x11, x12, x13, x20, x21, x22, x23, x30, x31, x32, x33]
plain index:     0    1    2    3    4    5    6    7    8    9   10   11   12   13   14   15
```
Начальные позиции: для `l` это `{0,0}`, для `r` это `{column_length - 1, row_length - 1} + 1`. 
```text

l = (i * row_length) + j = (0 * row_length) + 0 = 0; 
r = (i * row_length) + j = ((column_length - 1) * row_length) + (row_length - 1) + 1 = (column_length - 1) * row_length + row_length = column_length * row_length;
```
Ищем середину по индексу plain массива, найдя середину трансформируем индекс в 2d точку
и проверяем больше она или меньше и двигаем указатели на индексы соответственно. Ответ будет лежать
в левом индекс/левой точке. Найдя нужный левый индекс в plain массиве мы трансформируем
левый индекс plain массива в точку в матрице и получаем ответ.
