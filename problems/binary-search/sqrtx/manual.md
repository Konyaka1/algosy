### Solution
Solution with only int
```java
class Solution {
    public int mySqrt(int x) {
        int l = 0;
        int r = 46341;

        while (r - l > 1) {
            int m = l + (r - l) / 2;

            if (this.isGood(x, m)) {
                l = m;
            } else {
                r = m;
            }
        }

        return l;
    }

    private boolean isGood(int x, int m) {
        return m * m <= x;
    }
}
```
Solutions with long
```java
class Solution {
    public int mySqrt(int x) {
        long l = 0;
        long r = 1L + x;

        while (r - l > 1) {
            long m = (r + l) / 2;

            if (this.isGood(x, m)) {
                l = m;
            } else {
                r = m;
            }
        }

        return (int) l;
    }
    
    private boolean isGood(int x, long m) {
        return m * m <= x;
    }
}
```
### Time
O(log N) -- Делаем бинарный поиск
### Memory
O(1) -- Доп память не нужна
### Explication
Делаем бинарный поиск. Так как число лежит от 0 до _MAX_INT_, нам нужно быть
аккуратным с переполнением. Один из вариантов использовать long и в конце привести все к int.
Или же использовать поиск по максимальному возможному числу. Мы знаем, что `MAX_INT == 46340.9500011`
Значит максимально возможной ответ это 46340. при m = 46340, `m * m == 2147395600`, что 
меньше чем _MAX_INT_. Значит мы можем поставить l = 0, r = 46341, таким образом
у мы избежим переполнения int.
