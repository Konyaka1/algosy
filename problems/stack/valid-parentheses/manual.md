### Solution
```java
class Solution {
    public boolean isValid(String s) {
        Map<Character, Character> map = new HashMap<>() {{
            put('(', ')');
            put('{', '}');
            put('[', ']');
        }};

        Deque<Character> deq = new ArrayDeque<>();
        for (char ch : s.toCharArray()) {
            if (map.containsKey(ch)) {
                deq.offerLast(ch);
                continue;
            }

            if (deq.isEmpty()) {
                return false;
            }

            Character open = deq.pollLast();
            Character close = map.get(open);
            if (!close.equals(ch)) {
                return false;
            }
        }

        return deq.isEmpty();
    }
}
```
### Time
O(N) -- Проходим по строке один раз
### Memory
O(N) -- Для хранения открытых скобок
### Explication
Проходим по строке и добавляем в стек все открывающие скобки.
Как только мы нашли закрывающую скобку надо проверить такого ли она типа
как вершина стека.
