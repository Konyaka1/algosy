### Solution
```java
class MyQueue {

    // allowed methods
    // isEmpty()
    // offerLast()
    // peekLast()
    // pollLast()
    // size()

    final LinkedList<Integer> in = new LinkedList<>();
    final LinkedList<Integer> out = new LinkedList<>();

    public MyQueue() {

    }

    public void push(int x) {
        this.in.offerLast(x);
    }

    public int pop() {
        this.moveElements();
        return out.pollLast();
    }

    public int peek() {
        this.moveElements();
        return out.peekLast();
    }

    private void moveElements() {
        if (out.isEmpty() && !in.isEmpty()) {
            while (!in.isEmpty()) {
                out.offerLast(in.pollLast());
            }
        }
    }

    public boolean empty() {
        return in.isEmpty() && out.isEmpty();
    }
}
```
### Time
O(1) -- для всех операций в среднем
### Memory
O(N) -- структура данных хранит только элементы добавленные
### Explication
Создаем два стека, `in` and `out`. В принимающий стек всегда запихиваем новые элементы.
Теперь чтобы достать элемент, мы не можем взять его из `in`, потому что он возвращает последний вставленный, а не первый
Для этого "переливаем" все элементы в стек `out`, таким образом элементы в стеке `out` имеют
правильный порядок для операции `pop` и `peek`. Так и делаем переливание если `out` пустой.
