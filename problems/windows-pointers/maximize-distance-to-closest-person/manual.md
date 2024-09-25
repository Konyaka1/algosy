### Solution
```java
class Solution {
    public int maxDistToClosest(int[] seats) {
        int l = 0;
        int r = 0;

        int maxLength = 0;

        while (l < seats.length) {

            while (r + 1 < seats.length && seats[r + 1] == seats[r]) {
                r = r + 1;
            }

            if (seats[r] == 0) {

                int curLength = r - l + 1;

                if (r + 1 != seats.length && l != 0) {
                    curLength = (curLength + 1) >> 1;
                }

                maxLength = Math.max(maxLength, curLength);
            }
            l = r + 1;
            r = r + 1;
        }

        return maxLength;
    }
}
```
### Time
O(N) -- проходим по массиву один раз
### Memory
O(1) -- храним только два указателя
### Explication
Используем патерн окон, чтобы найти последовательность 0.
Найдя последовательность, смотрим является ли она крайней слева или крайней справа.
Если она крайняя -- текущая длина равна расстоянию между позициями индексами.
Если последовательность нулей имеет 1 с двух сторон, то длину надо разделить на 2 с округлением вверх.
