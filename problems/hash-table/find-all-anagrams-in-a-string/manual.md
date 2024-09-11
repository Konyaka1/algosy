### Solution
Time: 27:52
```java
class Solution {
    public List<Integer> findAnagrams(String s, String p) {
        if (p.length() > s.length()) {
            return Collections.emptyList();
        }
        
        char[] requiredAnagram = new char[26];
        char[] curAnagram = new char[26];

        for (int i = 0; i < p.length(); i++) {
            char pSymbol = p.charAt(i);
            requiredAnagram[pSymbol - 'a']++;

            char sSymbol = s.charAt(i);
            curAnagram[sSymbol - 'a']++;
        }

        List<Integer> result = new LinkedList<>();

        for (int i = 0; i <= s.length() - p.length(); i++) {
            if (equalsAnagrams(requiredAnagram, curAnagram)) {
                result.add(i);
            }

            int nextIndex = i + p.length();
            if (nextIndex < s.length()) {
                char next = s.charAt(nextIndex);
                curAnagram[next - 'a']++;

                char prev = s.charAt(i);
                curAnagram[prev - 'a']--;
            }
        }

        return result;
    }

    private boolean equalsAnagrams(char[] anagram1, char[] anagram2) {
        return Arrays.equals(anagram1, anagram2);
    }
}
```

### Time
O(N) -- потому что проходим по длине всей строки
### Memory
O(1) -- потому что используем массивы char фиксированной длины
### Explication
Изначально проверяем длину p. Если она больше чем s, то возвращаем пустой массив. 
Далее создаем id анаграммы как массив char[]. 
Нам нужна текущаю анаграммы длины p в строке s, и нужна анаграмма самой строки p.
Инициализируем current и required. 

Итерируем s столько, сколько физически возможно, то есть включительно s.length() - p.length().
Перед следующей итерацией отнимаем I элемент (это начало текущей анаграммы).
И также прибавляем I + p.length() элемент, это новый конец следующей анаграммы. Остальные символы в анаграмме остаются

a b c d e f g == s, p.length() == 3

Example iterations:
1) current substring [a, b, c]. anagram is [a -> 1, b -> 1, c -> 1]. делаем сдвиг, убираем первый и добавляем последний
2) current sybstring [b, c, d]. anagram is [b -> 1, c -> 1, d -> 1]. 
