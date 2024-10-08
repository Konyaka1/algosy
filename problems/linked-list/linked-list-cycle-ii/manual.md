### Solution
```java
public class Solution {
    public ListNode detectCycle(ListNode head) {
        ListNode slow = head;
        ListNode fast = head;

        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;

            if (slow == fast) {
                slow = head;
                while (slow != fast) {
                    slow = slow.next;
                    fast = fast.next;
                }
                return slow;
            }
        }

        return null;
    }
}
```
### Time
O(N) -- Проходим по всему списку
### Memory
O(1) -- Не используем доп память
### Explication
Используем Floyd’s Cycle Detection Algorithm. Найдя цикл
ставим один из указателей в начало и двигаемся по одному. Таким образом мы придем
в начало цикла.
Если мы не нашли цикл возвращаем null.
