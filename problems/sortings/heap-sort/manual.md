### Solution
```java
class Solution {
    public int[] sortArray(int[] nums) {
        MyHeap heap = new MyHeap(nums);

        for (int i = 0; i < nums.length; i++) {
            int max = heap.pop();
            nums[nums.length - 1 - i] = max;
        }

        return nums;
    }

    class MyHeap {

        public int[] heap;
        private int size;
        private final int minSize = 16;

        public MyHeap(int[] arr) {
            this.heap = arr;
            this.size = arr.length;
            for (int i = size / 2; i >= 0; i--) {
                siftDown(i);
            }
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
        }

        public int pop() {
            int top = heap[0];
            heap[0] = heap[size - 1];

            siftDown(0);

            size--;

            return top;
        }

        private void siftUp(int last) {
            if (last == 0) {
                return;
            }
            int parent = (last - 1) / 2;

            if (heap[parent] < heap[last]) {
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
            if (right < size && heap[right] > heap[left]) {
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
    }
}
```
### Time
O(N * log N) -- потому что 
### Memory
O(logN) -- для рекурсивной версии, O(1) -- для итеративной
### Explication
Применяем heapify для массива, используя кучу на максимум. O(N)

Затем достаем элемент из кучи и ставим его как последний элемент. O(logN)
