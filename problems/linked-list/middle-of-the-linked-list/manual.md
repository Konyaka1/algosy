### Solution
Подход с подсчетом длины
```java
class Solution {
    public ListNode middleNode(ListNode head) {
        int length = 0;

        ListNode cur = head;

        while (cur != null) {
            length++;
            cur = cur.next;
        }

        length = length / 2;
        cur = head;

        while (length > 0) {
            cur = cur.next;
            length--;
        }

        return cur;
    }
}
```
Подход с двумя указателями
```java
class Solution {
    public ListNode middleNode(ListNode head) {
        ListNode fast = head;
        ListNode slow = head;

        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }

        return slow;
    }
}
```
### Time
O(N) -- потому что надо пройти весь лист
### Memory
O(1) -- не нужна доп память
### Explication
Нужно найти середину -- для этого находим всю его длину. Для четной длины мы возвращаем
_второй_ элемент в середине. 
```text
1 solution
    1 2 3 4 5, length = 5, so k = length / 2 = 2
    we do two steps and return pointer
    
    1 2 3 4 5 6, length = 6, so k = length / 2 = 3
    we do 3 steps and return pointer
```
Также есть решение с двумя указателями, один быстрый, второй медленный. Медленный делает один шаг,
быстрый делает два шага. Быстрый ходит, пока он сам или следующий не равен `null`.
```text
2 solution
    s
    1 2 3 4 5 null        while (f != null && f.next != null) 
    f
    
      s
    1 2 3 4 5 null      
        f
        
        s
    1 2 3 4 5 null      f.next == null --> quit and return slow.
            f


    s
    1 2 3 4 5 6 null
    f
    
      s
    1 2 3 4 5 6 null
        f
            
        s
    1 2 3 4 5 6 null  f != null and f.next != null --> continue
            f
    
          s        
    1 2 3 4 5 6 null    f == null --> quit, return slow
                 f   
```
