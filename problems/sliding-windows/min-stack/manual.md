### Solution
```java
class MinStack {

    class Entry {
        int val;
        int min;
        Entry prev = null;
    }

    Entry head = null;

    public MinStack() {

    }

    public void push(int val) {
        Entry entry = new Entry();
        entry.val = val;
        entry.min = Math.min(val, this.getMin());
        entry.prev = head;
        head = entry;
    }

    public void pop() {
        head = head.prev;
    }

    public int top() {
        return head.val;
    }

    public int getMin() {
        if (head == null) {
            return Integer.MAX_VALUE;
        }
        return head.min;
    }
}
```
### Time
O(1) -- все операции O(1), память для операций O(1)
### Memory
O(N) -- память всей структуры данных занимает столько же, сколько элементов
### Explication
Храним указатель на вершину стека. В качестве entry мы храним 
текущее значение и максимум всего стека и ссылку на предыдущее значение.
При добавлении элемента мы обновляем голову (ссылку на `head`) и обновляем максимум.
При операции `peek` просто возвращаем максимум из головы.
При удалении говорим что голова это предыдущий элемент. 
