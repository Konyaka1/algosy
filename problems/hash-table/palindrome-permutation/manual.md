### Solution
```java
class Solution {
    public boolean canPermutePalindrome(String s) {
        boolean canHaveOdd = s.length() % 2 != 0;

        int[] freq = new int[26];
        for (char symbol : s.toCharArray()) {
            freq[symbol - 'a']++;
        }

        for (int curFreq : freq) {
            boolean isOdd = curFreq % 2 != 0;
            if (isOdd && canHaveOdd) {
                canHaveOdd = false;
            } else if (isOdd && !canHaveOdd) {
                return false;
            }
        }

        return true;
    }
}
```

### Time
O(N) -- потому что проходим по всей строке чтобы собрать все частоты
### Memory
O(1) -- потому что вся память константна, потому что набор букв ограничен
### Explication
Чтобы собрать из строки палиндром, нужно иметь четное кол-во повторений символов. И можно иметь один единственный 
элемент нечетной длины. Но только в одном случае, когда длина строки нечетна.

Создаем перменную, которая говорит, можно ли иметь нечетный символ. 
Как только находим нечетную длину и нечетную длину нельзя иметь возвращаем false.