### Solution
Sliding window
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
Basic solution
```java
class Solution {
    public int maxPower(String s) {
        int currentLength = 1;
        int maxLength = 0;

        int i = 0;
        while (i + 1 < s.length()) {
            if (s.charAt(i) == s.charAt(i + 1)) {
                currentLength++;
            } else {
                maxLength = Math.max(maxLength, currentLength);
                currentLength = 1;
            }
            i++;
        }

        return Math.max(maxLength, currentLength);
    }
}
```
### Time
O(N) -- Проходим по всей строке один раз 
### Memory
O(1) -- Не храним доп память
### Explication
Решение на sliding window. Ищем наибольшее окно.

Для обычного решения увеличиваем счетчик пока символы одинаковые, затем обновляем 
максимум
