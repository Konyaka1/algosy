### Solution
```java
class Solution {
    public boolean isPerfectSquare(int num) {
        long l = 0L;
        long r = 1L + num;

        while (r - l > 1) {
            long m = (l + r) / 2;

            if (this.isGood(m, num)) {
                l = m;
            } else {
                r = m;
            }
        }

        return l * l == num;
    }

    private boolean isGood(long m, int num) {
        return m * m <= num;
    }
}
```
```java
class Solution {
    public boolean isPerfectSquare(int num) {
        int l = 0;
        int r = 46341;

        while (r - l > 1) {
            int m = (l + r) / 2;

            if (this.isGood(m, num)) {
                l = m;
            } else {
                r = m;
            }
        }

        return l * l == num;
    }

    private boolean isGood(int m, int num) {
        return m * m <= num;
    }
}
```
### Time
O(log N) -- Делаем бинарный поиск 
### Memory
O(1) -- Фиксированная доп память
### Explication
Идея такая же как и в sqrtx, только в конце мы сравниваем l ^ 2 с числом num.