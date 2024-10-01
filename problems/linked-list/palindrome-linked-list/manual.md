### Solution
```java
class Solution {
    public boolean isPalindrome(ListNode head) {
        ListNode cur = head;
        ListNode prev = null;
        ListNode fast = head;

        while (fast != null && fast.next != null) {
            fast = fast.next.next;

            ListNode newNext = cur.next;

            cur.next = prev;

            prev = cur;

            cur = newNext;
        }

        if (fast != null) {
            cur = cur.next;
        }

        while (cur != null) {
            if (cur.val != prev.val) {
                return false;
            }
            cur = cur.next;
            prev = prev.next;
        }

        return true;
    }
}
```
### Time
O(N) -- Проходим по всему списку
### Memory
O(1) -- нет необходимости в доп памяти
### Explication
Идея заключается в использовании предыдущих задач _Middle of the linked list_ и 
_Reverse linked list_. Мы реверсим первую часть листа и затем делаем сравнение.
Важно не забыть подвинуть curr на один шаг, если быстрый не равен null. Это случай нечетной длины листа.
```text
Четная длина
p     c
null  1 -> 2 -> 3 -> 3 -> 2 -> 1 -> null
      f

    first iteration

          p    c
null  <-  1    2 -> 3 -> 3 -> 2 -> 1 -> null
                    f

              p    c
null <-  1 <- 2    3 -> 3 -> 2 -> 1 -> null
                             f

                  p    c
null <- 1 <- 2 <- 3    3 -> 2 -> 1 -> null  f == null --> quit.
                                       f
```
```text
Нечетная длина
p      c
null   1 -> 2 -> 3 -> 4 -> 3 -> 2 -> 1 -> null
       f

        p    c
null <- 1    2 -> 3 -> 4 -> 3 -> 2 -> 1 -> null
                  f

             p    c
null <- 1 <- 2    3 -> 4 -> 3 -> 2 -> 1 -> null
                            f

                  p    c
null <- 1 <- 2 <- 3    4 -> 3 -> 2 -> 1 -> null    f.next = null --> quit.
                                      f
```
