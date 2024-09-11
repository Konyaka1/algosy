### Solution
```java
class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {

        Map<String, List<String>> groupedStrs = new HashMap<>();

        for (String curStr : strs) {
            String anagramId = getAnagramId(curStr);

            List<String> group = groupedStrs.get(anagramId);
            if (group == null) {
                group = new LinkedList<>();
                groupedStrs.put(anagramId, group);
            }

            group.add(curStr);
        }

        return groupedStrs.values().stream().toList();
    }

    private String getAnagramId(String str) {
        char[] anagram = new char[26];

        for (char symbol : str.toCharArray()) {
            anagram[symbol - 'a']++;
        }

        return new String(anagram);
    }
}
```

### Time
O(N*K), N --> length of array, K --> length of longest string
### Memory
O(N*K), N --> length of array, K --> length of longest string
### Explication
Проходим по каждой строке и создаем ее anagram id. В данном случае я использовал массив char
и из этого массива строку.

Далее пихаем в map по id. Если такой ключ уже есть, то добавляем в значение (в лист).
Если такого ключа нет, создаем лист и присваиваем ему новый лист.