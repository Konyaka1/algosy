### Solution
TIME: ~10min.
```java
class Solution {
    public int diagonalSum(int[][] mat) {
        int result = 0;
        if (mat.length % 2 != 0) {
            int moyenIndex = mat.length >> 1;
            result = result - mat[moyenIndex][moyenIndex];
        }

        for (int i = 0; i < mat.length; i++) {
            result = result + mat[i][i] + mat[i][mat.length - 1 - i];
        }

        return result;
    }
}
```
### Time
O(N) -- проходим от 0 до длины массива один раз
### Memory
O(1) -- храним только переменную для результата
### Explication
Считаем сумму всех элементов по диагонали.

`mat[i][i]` -- главная диагональ, `mat[i][n - 1 - i]` -- вторичная диагональ.

Считаем суммы этих элементов в цикле. Главное не забыть вычесть элемент по середине, если матрица нечетной длины

