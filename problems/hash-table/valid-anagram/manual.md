### Solution
```java
class Solution {
    public boolean isAnagram(String s, String t) {
        if (s.length() != t.length()) {
            return false;
        }

        int[] freqs = new int[26];

        for (int i = 0; i < s.length(); i++) {
            int sChar = s.charAt(i);
            int tChar = t.charAt(i);

            freqs[sChar - 'a']++;
            freqs[tChar - 'a']--;
        }

        for (int curFreq : freqs) {
            if (curFreq != 0) {
                return false;
            }
        }

        return true;
    }
}
```

### Time
O(N) -- потому что проходим через всю длину строки
### Memory
O(1) -- потому что храним только массив с 26 интами
### Explication
Основные тейки по памяти
1) Не нужно создавать мапу, потому что символов всего 26. Достаточно массива
2) Не нужно создавать две мапы/массива. Достаточно одного; Одна строка отнимает, вторая прибавляет
### Note
НЕ ТОРОПИСЬ ДАЖЕ ЕСЛИ РЕШАЛ И ОБРАЩАЙ ВНИМАНИЕ НА CONSTRAINTS