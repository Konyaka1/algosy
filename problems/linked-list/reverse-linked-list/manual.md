### Solution
```java
class Solution {
    public ListNode reverseList(ListNode head) {
        ListNode prev = null;
        ListNode curr = head;

        while (curr != null) {
            ListNode newNext = curr.next;

            curr.next = prev;

            prev = curr;

            curr = newNext;
        }

        return prev;
    }
}
```
### Time
O(N) -- проходим по всему листу
### Memory
O(1) -- не используется доп память
### Explication
Проходим по списку и меняем связи. Говорим что текущий это голова, а предыдущий это `null`.
Начинаем менять связи в 4 действия пока текущий не равен null
1. Запоминаем `newNext =  cur.next`
2. Меняем связь текущего `cur.next = prev`
3. Говорим что предыдущий это текущий `prev = cur`
4. Говорим что текущий это новый след с шага _1_ `cur = newNext`
Базовая визуализация шагов
```text
Дано: 1 ----> 2 ----> 3 ----> null

0 шаг, ставим текущий и предыдущий
prev     curr    
null       1 ----> 2 ----> 3 ----> null

1 шаг
prev     curr    newNext
null       1 ----> 2 ----> 3 ----> null

2 шаг
prev     curr    newNext
null <---- 1        2 ----> 3 ----> null

3 шаг
         prev
         curr    newNext
null <---- 1        2 ----> 3 ----> null

4 шаг
         prev     curr
null <---- 1        2 ----> 3 ----> null
```
**Вторая итерация**
```text
имеем
         prev     curr
null <---- 1        2 ----> 3 ----> null

1 шаг
         prev     curr    newNext
null <---- 1        2 ----> 3 ----> null

2 шаг
         prev     curr    newNext
null <---- 1 <---- 2       3  ----> null

3 шаг
                 prev
                 curr    newNext
null <---- 1 <---- 2       3  ----> null

4 шаг
                 prev    curr
null <---- 1 <---- 2       3  ----> null
```
**Последняя**
```text
имеем
                 prev    curr
null <---- 1 <---- 2       3  ----> null

1 шаг
                 prev    curr      newNext
null <---- 1 <---- 2       3  ----> null 

2 шаг
                 prev    curr      newNext
null <---- 1 <---- 2 <---- 3        null

3 шаг
                         prev
                         curr      newNext
null <---- 1 <---- 2 <---- 3        null

4 шаг
                         prev       curr
null <---- 1 <---- 2 <---- 3        null
```
