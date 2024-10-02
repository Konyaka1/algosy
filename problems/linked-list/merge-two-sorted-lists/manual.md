### Solution
```java
class Solution {
    public ListNode mergeTwoLists(ListNode list1, ListNode list2) {
        ListNode dummy = new ListNode();

        ListNode cur1 = list1;
        ListNode cur2 = list2;

        ListNode cur = dummy;

        while (cur1 != null && cur2 != null) {
            ListNode newNode = null;
            if (cur1.val < cur2.val) {
                newNode = new ListNode(cur1.val);
                cur1 = cur1.next;
            } else {
                newNode = new ListNode(cur2.val);
                cur2 = cur2.next;
            }
            cur.next = newNode;
            cur = newNode;
        }

        while (cur1 != null) {
            ListNode newNode = new ListNode(cur1.val);
            cur.next = newNode;
            cur = newNode;

            cur1 = cur1.next;
        }

        while (cur2 != null) {
            ListNode newNode = new ListNode(cur2.val);
            cur.next = newNode;
            cur = newNode;

            cur2 = cur2.next;
        }

        return dummy.next;
    }
}
```
### Time
O(n + m) -- n,m длины списков, мы проходим по двум спискам
### Memory
O(n + m) -- память для создания ответа
### Explication
Проходим по двум спискам двумя указателями, и двигаем тот, что меньше. Меньшее число
добавляем как ноду в ответ. Чтобы избежать _if else_ в начале, создаем **dummy** ноду, 
у которой следующий узел это голова нового списка
