### Solution
```java
public class Solution {

    public int lengthOfLongestSubstringKDistinct(String s, int k) {
        if (k < 1) {
            return 0;
        }

        int l = 0;
        int r = -1;
        Map<Character, Integer> freq = new HashMap<>();

        int maxLength = 0;
        while (r + 1 < s.length()) {
            while (this.tryOffer(r + 1, s, k, freq)) {
                r = r + 1;
            }

            maxLength = Math.max(maxLength, r - l + 1);

            char leftCh = s.charAt(l);
            int leftChFreq = freq.get(leftCh);
            if (leftChFreq == 1) {
                freq.remove(leftCh);
            } else {
                freq.put(leftCh, leftChFreq - 1);
            }
            l = l + 1;
        }

        return maxLength;
    }

    private boolean tryOffer(int r, String s, int k, Map<Character, Integer> freq) {
        if (r >= s.length()) {
            return false;
        }

        char curCh = s.charAt(r);
        if (freq.containsKey(curCh) || freq.size() < k) {
            freq.merge(curCh, 1, Integer::sum);
            return true;
        }

        return false;
    }
}
```
### Time
O(N) -- потому что проходим по строке один раз
### Memory
O(K) -- храним кол-во вхождений каждого символа
### Explication
Решаем методом пересекающихся окон. Состояние окна это кол-во повторений
каждого символа. Переставляем правый указатель, если размер мапы позволяет или если это уже
встреченный символ. При перемещении левого указателя нужно отнять кол-во повторений у левого
символа. Если кол-во повторений 0 -- удаляем его из мапы.
