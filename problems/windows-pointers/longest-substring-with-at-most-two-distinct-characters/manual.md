### Solution
```java
public class Solution {

    public int lengthOfLongestSubstringTwoDistinct(String s) {
        int l = 0;
        int r = -1;

        Map<Character, Integer> charLastPos = new HashMap<>();
        int maxLength = 0;
        while (r + 1 < s.length()) {
            while (this.tryOffer(r + 1, s, charLastPos)) {
                r = r + 1;
            }

            maxLength = Math.max(maxLength, r - l + 1);

            int min = s.length() + 1;
            Character charToRemove = null;
            for (Map.Entry<Character, Integer> entry : charLastPos.entrySet()) {
                if (entry.getValue() < min) {
                    charToRemove = entry.getKey();
                    min = entry.getValue();
                }
            }
            charLastPos.remove(charToRemove);
            l = min + 1;
        }

        return maxLength;
    }

    private boolean tryOffer(int r, String s, Map<Character, Integer> charLastPos) {
        if (r >= s.length()) {
            return false;
        }

        char ch = s.charAt(r);
        if (charLastPos.containsKey(ch) || charLastPos.size() < 2) {
            charLastPos.put(ch, r);
            return true;
        }

        return false;
    }
}
```
### Time
O(N) -- Проходим по всей строке один раз 
### Memory
O(1) -- храним только два элемента в мапе и их индексы.
### Explication
Проходим по всей строке метод пересекающихся окон. Состояние окна -- это
символы в текущей подстроке и их последние индексы. 

Покажу на примере:
По алгоритму мы двигаем правый указатель, пока кол-во ключей в мапе меньше 2, 
иными словами, пока кол-во уникальных символов в подстроке меньше 2.
Подвинув указатели мы запомнили что `{a: 4, b: 9}`.
```text
l
0 1 2 3 4 5 6 7 8 9 10
a a a b a b b b b b c  cccccccccccccc
                  r
```
Теперь куда мы можем подвинуть `l`? Мы можем пропустить все символы `a` и 
поставить левый указатель на позицию 5. То есть мы двигаем левый указатель
до минимальной позиции в мапе + 1.
```text
          l
0 1 2 3 4 5 6 7 8 9 10
a a a b a b b b b b c  cccccccccccccc
                  r
```
Таким образом, мы пропустили все предыдущий `a` и имеем подстроку только из `b` и можем
дальше двигать правый указатель.