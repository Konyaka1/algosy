### Solution
```java
class Solution {
    public int[] dailyTemperatures(int[] temperatures) {
        int[] res = new int[temperatures.length];

        Deque<TempIndex> deq = new ArrayDeque<>();
        for (int i = 0; i < temperatures.length; i++) {
            while (!deq.isEmpty() && temperatures[i] > deq.peekLast().val) {
                TempIndex ti = deq.pollLast();
                res[ti.index] = i - ti.index;
            }
            deq.offerLast(new TempIndex(temperatures[i], i));
        }

        return res;
    }

    class TempIndex {
        int val;
        int index;

        public TempIndex(int val, int index) {
            this.val = val;
            this.index = index;
        }
    }
}
```
### Time
O(N) -- Проходим по температурам один раз
### Memory
O(N) -- Для ответа, и в худшем случае в стеке будут лежать все температуры
### Explication
Проходим по температурам и пихаем в стек температуру и ее индекс.
Если новый элемент больше чем голова стека --> мы нашли ответ для головы стека.
Достаем голову и запихиваем в ответ разницу между индексами. 

**Note**: можно в стек засовывать только индекс элемента, тогда в while мы 
будем сравнивать `temp[i]` и `temp[stack.top]`.
