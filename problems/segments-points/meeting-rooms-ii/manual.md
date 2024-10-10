### Solution
```java
class Solution {
    public int minMeetingRooms(int[][] intervals) {
        Comparator<int[]> comp = (a, b) -> {
            if (a[0] == b[0]) {
                return a[1] - b[1];
            } else {
                return a[0] - b[0];
            }
        };
        PriorityQueue<int[]> queue = new PriorityQueue<>(comp);

        for (int[] interval : intervals) {
            queue.offer(new int[]{interval[0], 1});
            queue.offer(new int[]{interval[1], -1});
        }

        int max = 0;
        int cur = 0;
        while (!queue.isEmpty()) {
            cur += queue.poll()[1];
            max = Math.max(cur, max);
        }

        return max;
    }
}
```
### Time
O(N logN) -- Используется приоритетная очередь для сортировки элементов.
### Memory
O(N) -- Хранятся все точки в очереди.
### Explication

