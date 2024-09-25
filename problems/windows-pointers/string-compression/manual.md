### Solution
```java
class Solution {
    public int compress(char[] chars) {
        int l = 0;
        int r = 0;

        int resultIndex = 0;

        while (l < chars.length) {
            while (r + 1 < chars.length && chars[r + 1] == chars[r]) {
                r = r + 1;
            }

            int length = r - l + 1;

            chars[resultIndex] = chars[l];
            resultIndex = resultIndex + 1;

            if (length > 1) {
                char[] number = Integer.toString(length).toCharArray();
                for (char digit : number) {
                    chars[resultIndex] = digit;
                    resultIndex++;
                }
            }

            l = r + 1;
            r = r + 1;
        }

        return resultIndex;
    }
}
```
### Time
O(N) -- проходим по массиву один раз
### Memory
O(1) -- храним только два указателя
### Explication
Используем паттерн окон, чтобы найти текущую последовательность символов. 
Найдя последовательность, смотрим на ее длину и ставим нужные символы в правильные места.
