## Fails
### 1st try
Forgot one скобка
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
         else { // HERE, have no idea how
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