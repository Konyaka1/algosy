### Solution
```java
class Solution {
    public String simplifyPath(String path) {
        Deque<String> deq = new ArrayDeque<>();
        for (String str : path.split("/")) {
            if (str.length() == 0 || ".".equals(str)) {
                continue;
            }
            if ("..".equals(str)) {
                deq.pollLast();
            } else {
                deq.offerLast(str);
            }
        }

        if (deq.isEmpty()) {
            return "/";
        }

        StringBuilder sb = new StringBuilder();
        while (!deq.isEmpty()) {
            sb.append("/");
            sb.append(deq.pollFirst());
        }
        return sb.toString();
    }
}
```
### Time
O(N) -- Проходим по всей строке один раз 
### Memory
O(N) -- В стек надо запихнуть все элементы строки
### Explication
Пихаем в стек, потому что с помощью стека будет легко удалять
части пути при нахождении `..`
