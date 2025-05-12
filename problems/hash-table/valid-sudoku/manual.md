### Solution
```go
func isValidSudoku(board [][]byte) bool {
    rows := [9][9]bool{}
    columns := [9][9]bool{}
    squares := [9][9]bool{}
    
    for i := range 9 {
        for j := range 9 {
            if board[i][j] == '.' {
                continue
            }
            
            num := board[i][j] - '1'
            sqID := (i / 3) * 3 + (j / 3)
            if rows[i][num] || columns[j][num] || squares[sqID][num] {
                return false
            }
            
            rows[i][num] = true
            columns[j][num] = true
            squares[sqID][num] = true
        }
    }
    
    return true
}
```
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
        return (i / 3) * 3 + (j / 3);
    }
}
```
Оптмизированное решение на битовых операциях.
```c++
class Solution {
public:
    bool isValidSudoku(vector<vector<char>>& board) {
        __int128 rows = 0;
        __int128 columns = 0;
        __int128 boxes = 0;
 
        __int128 bit = 1;
 
        for (int i = 0; i < 9; i++) {
            for (int j = 0; j < 9; j++) {
                if (board[i][j] == '.') continue;
 
                int number = board[i][j] - '1';
 
                __int128 rowMask = bit << (i * 9 + number);
                if (rows & rowMask) {
                    return false;
                } else {
                    rows = rows | rowMask;
                }
 
                __int128 columnMask = bit << (j * 9 + number);
                if (columns & columnMask) {
                    return false;
                } else {
                    columns = columns | columnMask;
                }
 
                int boxId = (i / 3) * 3 + (j / 3);
                __int128 boxMask = bit << (number + (boxId * 9));
                if (boxes & boxMask) {
                    return false;
                } else {
                    boxes = boxes | boxMask;
                }
            }
        }
 
        return true;
    }
};
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
### Note
Сущесвует спобос проще, чтобы достать индекс квадарата
``int blockIdx = (i / 3) * 3 + (j / 3);``
### Note
в мапу можно класть такой тип `[2]int` и он будет comparable и спокойно можно использовать как ключ