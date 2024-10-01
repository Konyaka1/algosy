### Solution
```java
class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        int[] result = new int[nums.length - k + 1];

        MaxFifo fifo = new MaxFifo();
        for (int i = 0; i < k; i++) {
            fifo.offer(nums[i]);
        }

        int l = 0;
        int r = k - 1;
        result[0] = fifo.max();
        for (int i = k; i < nums.length; i++) {
            fifo.poll();
            fifo.offer(nums[i]);
            result[i - k + 1] = fifo.max();
        }

        return result;
    }

    class MaxStack {
        class Entry {
            Entry prev;
            int val;
            int max;
        }

        Entry head = null;

        public MaxStack() {

        }

        public void offer(int val) {
            if (head == null) {
                head = new Entry();
                head.val = val;
                head.max = val;
                head.prev = null;
            } else {
                Entry entry = new Entry();
                entry.val = val;
                entry.max = Math.max(head.max, val);
                entry.prev = head;
                head = entry;
            }
        }


        public int max() {
            if (head == null) {
                return Integer.MIN_VALUE;
            }
            return head.max;
        }

        public int poll() {
            int val = head.val;
            head = head.prev;
            return val;
        }

        public boolean isEmpty() {
            return head == null;
        }
    }

    class MaxFifo {

        final MaxStack in = new MaxStack();
        final MaxStack out = new MaxStack();

        public MaxFifo() {

        }

        void offer(int val) {
            in.offer(val);
        }

        int max() {
            return Math.max(in.max(), out.max());
        }

        void poll() {
            moveElements();
            out.poll();
        }

        void moveElements() {
            if (!out.isEmpty()) {
                return;
            }
            while (!in.isEmpty()) {
                out.offer(in.poll());
            }
        }

    }
}
```
### Time
O(N) -- потому что проходим через массив один раз
### Memory
O(K) -- в MaxFifo храним только k элементов.
### Explication
Для решения задачи используем подход из задач _Min Stack_ и _Implement fifo using stacks_.
Зачем нам нужно fifo? Потому что в каждом окне мы убираем элемент, который был 
добавлен первым (начало окна) и добавляем новый элемент (правый конец). Теперь нам
нужно найти способ нахождения максимального элемента в fifo. 
Мы умеем строить стек, который за O(1) возвращает минимальынй элемент. Поэтому строим fifo
используя два _максимальных стека_ для очереди мы легко может найти текущее состояние окна.
