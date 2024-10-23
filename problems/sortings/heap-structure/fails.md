## Fails
### 1st try iterative
Forgot to add type for minSize variable
```java
class MyHeap {

    private int[] heap;
    private int size;
    private final minSize = 16; // HERE

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

        if (++this.size == this.heap.length) {
            this.expand();
        }
    }

    public int pop() {
        int top = this.peek();
        int last = this.heap[size - 1];
        this.heap[0] = last;

        this.siftDown();

        if (--this.size == this.length / 4) {
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

        while (true) {
            int left = top * 2 + 1;
            int right = top * 2 + 2;

            if (left >= size) {
                return;
            }

            int maxIndex = left;
            if (right < size && heap[right] > heap[left]) {
                maxIndex = right;
            }

            if (heap[top] >= heap[maxIndex]) {
                return;
            }

            swap(top, maxIndex);

            top = maxIndex;
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
### 2nd try iterative
Accidentally removed variable name
```java
class MyHeap {

    private int[] heap;
    private int size;
    private final int minSize = 16; // HERE

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

        if (++this.size == this.heap.length) {
            this.expand();
        }
    }

    public int pop() {
        int top = this.peek();
        int last = this.heap[size - 1];
        this.heap[0] = last;

        this.siftDown();

        if (--this.size == this.length / 4) { // HERE
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

        while (true) {
            int left = top * 2 + 1;
            int right = top * 2 + 2;

            if (left >= size) {
                return;
            }

            int maxIndex = left;
            if (right < size && heap[right] > heap[left]) {
                maxIndex = right;
            }

            if (heap[top] >= heap[maxIndex]) {
                return;
            }

            swap(top, maxIndex);

            top = maxIndex;
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
### 1st try recursive
Forgot to use array element by index, not the index itself
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

        if (parent > heap[last]) { // HERE
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

        if (heap[top] < heap[minIndex]) {
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
### 2nd try recursive
Messed up sift down method
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

        if (heap[top] < heap[minIndex]) { // HERE
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
