### Solution
```java
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode traverse = head;
        ListNode dummy = new ListNode();
        dummy.next = head;

        ListNode deleteNode = dummy;

        while (n > 0) {
            traverse = traverse.next;
            n--;
        }

        while (traverse != null) {
            traverse = traverse.next;

            deleteNode = deleteNode.next;
        }

        deleteNode.next = deleteNode.next.next;

        return dummy.next;
    }
}
```
### Time
O(N) -- необходимо пройтись по всему листу, чтобы знать его длину
### Memory
O(1) -- потому что используется фиксированное кол-во указателей
### Explication
Чтобы удалить какой-то узел с конца, надо знать длину листа. Для этого один из указателей должен
проходить по листу от начала до конца. Второй указатель идет с задержкой в n шагов и начинает с dummy узла
чтобы похэдлнить крайние случаи. Как только первый дойдет до конца, второй будет указывать
на ноду ДО необходимой ноды для удаления.

Примеры:
```text
n = 2, l = 7. we have to delete node with 6 value
start:
    d r         _
dummy 1 2 3 4 5 6 7 null

after moving first pointer n times
    d     r
dummy 1 2 3 4 5 6 7 null

after moving two pointers
              d     r
dummy 1 2 3 4 5 6 7 null   ---  5.next = 5.next.next == 7
```
```text
n = 7, l = 7. we have to delete node with 1 value
start:
    d r         
dummy 1 2 3 4 5 6 7 null

after moving first pointer n times
    d               r
dummy 1 2 3 4 5 6 7 null

after moving two pointers. r == null so actually we didn't move pointers here
    d               r
dummy 1 2 3 4 5 6 7 null   dummy.next = dummy.next.next == 2, and we return dummy.next as result
```
```text
n = 1, l = 7. we have to delete node with 7 value
start:
    d r           _
dummy 1 2 3 4 5 6 7 null

after moving first pointer n times
    d   r
dummy 1 2 3 4 5 6 7 null

after moving two pointers. r == null so actually we didn't move pointers here
                d   r
dummy 1 2 3 4 5 6 7 null   6.next = 6.next.next == null, and we return dummy.next as result
```
