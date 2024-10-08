### Solution
```java
public class Solution {
    public boolean hasCycle(ListNode head) {
        ListNode slow = head;
        ListNode fast = head;

        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;

            if (slow == fast) {
                return true;
            }
        }

        return false;
    }
}
```
### Time
O(N) -- потому что проходим по всем нодам
### Memory
O(1) -- не используется доп память
### Explication
Используется алгоритм Floyd’s Cycle Detection Algorithm.
