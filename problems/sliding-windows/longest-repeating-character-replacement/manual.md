### Solution
```java
class Solution {
    public int characterReplacement(String s, int k) {
        int l = 0;
        int r = -1;

        int max = 0;
        int[] freq = new int[26];
        int[] maxSubString = new int[1];
        while (r + 1 < s.length()) {
            while (this.canOffer(r + 1, l, s, k, freq, maxSubString)) {
                r = r + 1;
            }

            int curLength = r - l + 1;
            max = Math.max(max, curLength);

            char ch = s.charAt(l);
            freq[ch - 'A']--;

            l = l + 1;
        }

        return max;
    }

    private boolean canOffer(int r, int l, String s, int k, int[] freq, int[] maxSubString) {
        if (r >= s.length()) {
            return false;
        }
        char ch = s.charAt(r);
        int charFreq = freq[ch - 'A'] + 1;
        int tmpMax = Math.max(maxSubString[0], charFreq);

        if ((r - l + 1) - tmpMax <= k) {
            maxSubString[0] = tmpMax;
            freq[ch - 'A'] += 1;
            return true;
        } else {
            return false;
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
