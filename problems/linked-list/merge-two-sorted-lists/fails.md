## Fails
### 1st try
Error in syntax. Forgot to put NEW before constructor.
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
                newNode = ListNode(cur1.val); // HERE
                cur1 = cur1.next;
            } else {
                newNode = ListNode(cur2.val); // HERE
                cur2 = cur2.next;
            }
            cur.next = newNode;
            cur = newNode;
        }

        while (cur1 != null) {
            newNode = ListNode(cur1.val); // HERE
            cur.next = newNode;
            cur = newNode;

            cur1 = cur1.next;
        }

        while (cur2 != null) {
            newNode = ListNode(cur2.val); // HERE
            cur.next = newNode;
            cur = newNode;

            cur2 = cur2.next;
        }

        return dummy.next;
    }
}
```
### 2nd try
Error in syntax. Forgot to put class name for pointer before creation of new object.
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
            newNode = new ListNode(cur1.val); // HERE
            cur.next = newNode;
            cur = newNode;

            cur1 = cur1.next;
        }

        while (cur2 != null) {
            newNode = new ListNode(cur2.val); // HERE
            cur.next = newNode;
            cur = newNode;

            cur2 = cur2.next;
        }

        return dummy.next;
    }
}
```