### Solution
```java
class MinStack {

    final LinkedList<Integer> stack = new LinkedList<>();
    final LinkedList<Integer> dequeue = new LinkedList<>();

    public MinStack() {

    }

    public void push(int val) {
        this.stack.offerLast(val);
        int min = this.getMin();
        if (val <= min) {
            this.dequeue.offerFirst(val);
        } else {
            this.dequeue.offerLast(val);
        }
    }

    public void pop() {
        int top = this.stack.pollLast();
        int min = this.getMin();
        if (top == min) {
            this.dequeue.pollFirst();
        } else {
            this.dequeue.pollLast();
        }
    }

    public int top() {
        return this.stack.peekLast();
    }

    public int getMin() {
        if (this.dequeue.size() == 0) {
            return Integer.MAX_VALUE;
        }
        return this.dequeue.peekFirst();
    }
}
```

### Time
O(1) -- все операции O(1), память для операций O(1)
### Memory
O(N) -- память всей структуры данных занимает столько же, сколько элементов
### Explication
Создаем два списка -- один оригинальный стак, который и выполняет функцию очереди, и второй
список, который хранит первый элемент как минимальный.
Идея такова: если добавляется новый элемент, в стак он идет как обычно, а во второй список с проверкой:
Если новый элемент меньше минимума, то новый элемент становится вначало второго списка, иначе -- в конец.
Аналогичная ситуация с доставанием элемента -- если из стака достали минимальный элемент, то из списка убираем начало, 
иначе из списка убираем конец. Таким образом второй список всегда хранит минимальный элемент как первый.
