### Solution
Iterative approach
```java
class MyHeap {

    private int[] heap;
    private int size;
    private final int minSize = 16;

    public MyHeap() {
        this.heap = new int[minSize];
        this.size = 0;
    }

    public boolean isEmpty() {
        return this.size == 0;
    }

    public int peek() {
        return heap[0];
    }

    public void push(int number) {
        this.heap[size] = number;

        this.siftUp();
        
        this.size++;
        
        if (this.size == this.heap.length) {
            this.expand();
        }
    }

    public int pop() {
        int top = this.peek();
        int last = this.heap[size - 1];
        this.heap[0] = last;

        this.siftDown();

        this.size--;
        
        if (this.size == this.heap.length / 4) {
            this.collapse();
        }

        return top;
    }

    private void siftUp() {
        int last = size - 1;

        while (last > 0) {
            int parent = (last - 1) / 2;

            if (heap[parent] >= heap[last]) {
                return;
            }

            swap(last, parent);

            last = parent;
        }
    }

    private void siftDown() {
        int top = 0;
        int left = 1;
        int right = 2;

        while (left < size) {
            int maxIndex = left;
            if (right < size && heap[right] > heap[left]) {
                maxIndex = right;
            }

            if (heap[top] >= heap[maxIndex]) {
                return;
            }

            swap(top, maxIndex);

            top = maxIndex;
            left = top * 2 + 1;
            right = top * 2 + 2;
        }
    }

    private void swap(int l, int r) {
        int tmp = heap[l];
        heap[l] = heap[r];
        heap[r] = tmp;

    }

    private void expand() {
        int[] copy = new int[heap.length * 2];
        System.arraycopy(this.heap, 0, copy, 0, this.size);
        this.heap = copy;
    }

    private void collapse() {
        if (this.heap.length == minSize) {
            return;
        }
        int[] copy = new int[heap.length / 2];
        System.arraycopy(this.heap, 0, copy, 0, this.size);
        this.heap = copy;
    }
}
```
Recursive approach
```java
class MyHeap {

    public int[] heap;
    private int size;
    private final int minSize = 16;

    public MyHeap() {
        this.heap = new int[minSize];
        this.size = 0;
    }

    public boolean isEmpty() {
        return this.size == 0;
    }

    public int peek() {
        return heap[0];
    }

    public void push(int number) {
        heap[size] = number;

        siftUp(size);

        size++;
        if (size == heap.length) {
            expand();
        }
    }

    public int pop() {
        int top = heap[0];
        heap[0] = heap[size - 1];

        siftDown(0);

        size--;

        if (size == heap.length / 4) {
            collapse();
        }

        return top;
    }

    private void siftUp(int last) {
        if (last == 0) {
            return;
        }
        int parent = (last - 1) / 2;

        if (heap[parent] > heap[last]) {
            swap(parent, last);
            siftUp(parent);
        }

    }

    private void siftDown(int top) {
        int left = top * 2 + 1;
        int right = top * 2 + 2;
        if (left >= size) {
            return;
        }

        int minIndex = left;
        if (right < size - 1 && heap[right] < heap[left]) {
            minIndex = right;
        }

        if (heap[top] > heap[minIndex]) {
            swap(top, minIndex);
            siftDown(minIndex);
        }
    }

    private void swap(int l, int r) {
        int tmp = heap[l];
        heap[l] = heap[r];
        heap[r] = tmp;

    }

    private void expand() {
        int[] copy = new int[heap.length * 2];
        System.arraycopy(this.heap, 0, copy, 0, this.size);
        this.heap = copy;
    }

    private void collapse() {
        if (this.heap.length == minSize) {
            return;
        }
        int[] copy = new int[heap.length / 2];
        System.arraycopy(this.heap, 0, copy, 0, this.size);
        this.heap = copy;
    }
}
```
### Time
O(log n) -- для push и pop 
### Memory
O(n) -- кол-во элементов добавленных
### Explication

