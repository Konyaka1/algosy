### Solution
```java
class Solution {
    public int characterReplacement(String s, int k) {
        int l = 0;
        int r = -1;

        int maxLength = 0;
        int[] map = new int[26];
        int[] curMax = {0};
        while (r + 1 < s.length()) {
            while (this.canOffer(s, l, r + 1, k, map, curMax)) {
                r = r + 1;
            }

            maxLength = Math.max(r - l + 1, maxLength);

            map[s.charAt(l) - 'A']--;

            l = l + 1;
        }

        return maxLength;
    }

    private boolean canOffer(String s, int l, int r, int k, int[] map, int[] max) {
        if (r >= s.length()) {
            return false;
        }

        max[0] = Math.max(max[0], ++map[s.charAt(r) - 'A']);

        int curK = (r - l + 1) - max[0];
        if (curK > k) {
            map[s.charAt(r) - 'A']--;
            return false;
        } else {
            return true;
        }
    }
}
```
### Time
O(N) -- Проходим по всей строке один раз 
### Memory
O(K) -- Мапа фиксированной длины, не зависит от N.
### Explication
Мы не обновляем максимум freq при передвижении левого указателя, потому что
максимальная подстрока удовлетворяющая условию будет иметь
максимальное кол-во одинаковых символов.
