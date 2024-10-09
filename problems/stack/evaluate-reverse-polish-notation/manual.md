### Solution
```java
class Solution {
    public int evalRPN(String[] tokens) {
        Deque<Integer> deq = new ArrayDeque<>();

        for (int i = 0; i < tokens.length; i++) {
            if (tokens[i].length() == 1 && tokens[i].charAt(0) < 48) {
                int a = deq.pollLast();
                int b = deq.pollLast();
                char operation = tokens[i].charAt(0);
                int res;
                if (operation == '+') {
                    res = a + b;
                } else if (operation == '-') {
                    res = b - a;
                } else if (operation == '*') {
                    res = a * b;
                } else {
                    res = b / a;
                }
                deq.offerLast(res);
            } else {
                deq.offerLast( Integer.parseInt(tokens[i]));
            }
        }
        return deq.pollLast();
    }
}
```
### Time
O(N) -- Проходим по всем входным данным. 
### Memory
O(N) -- В худшем случае, чтобы хранить все числа в стеке
### Explication
Считаем обратную польскую запись. В стек всегда кладем число. На операции
достаем два числа из стека и применяем соответствующие вычисления. Результат кладем обратно в стек.

