### Solution
```java
class Solution {
    public int maxPower(String s) {
        int l = 0;
        int r = 0;

        int maxLength = 0;

        while (l < s.length()) {
            while (r + 1 < s.length() && s.charAt(r) == s.charAt(r + 1)) {
                r = r + 1;
            }

            maxLength = Math.max(maxLength, r - l + 1);

            l = r + 1;
            r = r + 1;
        }

        return maxLength;
    }
}
```
### Time
O(N) -- Проходим по всей строке один раз 
### Memory
O(1) -- Не храним доп память
### Explication
Решение на sliding window. Ищем наибольшее окно
