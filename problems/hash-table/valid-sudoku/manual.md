### Solution
```java
class Solution {
    public boolean isValidSudoku(char[][] board) {
        List<Set<Character>> lines = new ArrayList<>(9);
        List<Set<Character>> rows = new ArrayList<>(9);
        List<Set<Character>> squares = new ArrayList<>(9);

        for (int i = 0; i < 9; i++) {
            lines.add(new HashSet<>());
            rows.add(new HashSet<>());
            squares.add(new HashSet<>());
        }


        for (int i = 0; i < board.length; i++) {
            for (int j = 0; j < board[i].length; j++) {
                char currChar = board[i][j];
                if (currChar == '.') {
                    continue;
                }

                if (!lines.get(i).add(currChar)) {
                    return false;
                }

                if (!rows.get(j).add(currChar)) {
                    return false;
                }

                int square = getSquare(i, j);

                if (!squares.get(square).add(currChar)) {
                    return false;
                }
            }
        }

        return true;
    }

    private int getSquare(int i, int j) {
        if (i < 3 && j < 3) {
            return 0;
        }
        if (i < 3 && j < 6) {
            return 3;
        }
        if (i < 3) {
            return 6;
        }
        if (i < 6 && j < 3) {
            return 1;
        }
        if (i < 6 && j < 6) {
            return 4;
        }
        if (i < 6) {
            return 7;
        }
        if (j < 3) {
            return 2;
        }
        if (j < 6) {
            return 5;
        }
        return 8;

    }
}
```

### Time
O(N^2) -- потому что проходим по каждому элементу матрицы. Но n == 9, поэтому я наверное могу сказать
что это O(1)
### Memory
O(N) -- потому что храним каждый уникальный элемент в сете. Но n == 9, поэтому я наверное могу сказать
что это O(1)
### Explication
Решение задачи выглядит также как и в жизни. Нам надо проверить каждую строку/квадрат/столбец.

Чтобы не проходить 3 раза матрицу мы сохраняем каждый пройденный элемент в соотвествующий ему сет строки/столбца/квадрата.

Из неприятрного это определить номер индекс квадрата. Но это обычный if else на все варианты. 
Фиксируем сначала i < 3 и проходим по всем вариантам j. Затем фиксируем i < 6 и проходим по всем j.
В итоге все варианты i мы разобрали и мы знаем что он больше 6 и меньше 9. Соотвественно перебираем только j.
