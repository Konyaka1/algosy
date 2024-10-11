### Solution 1
With priority queue
```java
class Solution {
    public boolean carPooling(int[][] trips, int capacity) {
        Comparator<int[]> comp = (a, b) -> {
            if (a[0] == b[0]) {
                return Integer.compare(a[1], b[1]);
            } else {
                return Integer.compare(a[0], b[0]);
            }
        };

        PriorityQueue<int[]> queue = new PriorityQueue<>(trips.length * 2, comp);

        for (int[] trip : trips) {
            queue.offer(new int[]{trip[1], trip[0]});
            queue.offer(new int[]{trip[2], -trip[0]});
        }

        int curPass = 0;

        while (!queue.isEmpty()) {
            int[] point = queue.poll();
            curPass += point[1];
            if (curPass > capacity) {
                return false;
            }
        }

        return true;
    }
} 
```
### Time
O(N log N) -- потому что добавляем 2 * N точек в очередь со сложностью log N. Также достаем из очереди
со сложностью log N
### Memory
O(N) -- Проходим по всему массиву точек
### Solution 2
With array
```java
class Solution {
    public boolean carPooling(int[][] trips, int capacity) {
        Comparator<int[]> comp = (a, b) -> {
            if (a[0] == b[0]) {
                return Integer.compare(a[1], b[1]);
            } else {
                return Integer.compare(a[0], b[0]);
            }
        };

        int[][] points = new int[trips.length * 2][2];

        int i = 0;
        for (int[] trip : trips) {
            points[i++] = new int[] {trip[1], trip[0]};
            points[i++] = new int[] {trip[2], -trip[0]};
        }
        Arrays.sort(points, comp);

        int curPass = 0;
        for (int[] point : points) {
            curPass += point[1];
            if (curPass > capacity) {
                return false;
            }
        }

        return true;
    }
}
```
### Time
O(N log N) -- потому что сортируем массив точек длины 2 * N. Затем проходимся по всем
точкам длины 2 * N
### Memory
O(N) -- Проходим по всему массиву точек
### Solution 3
With array
```java
class Solution {
    public boolean carPooling(int[][] trips, int capacity) {
        int[] points = new int[1001];

        for (int[] trip : trips) {
            points[trip[1]] += trip[0];
            points[trip[2]] -= trip[0];
        }

        for (int pass : points) {
            capacity -= pass;
            if (capacity < 0) {
                return false;
            }
        }

        return true;
    }
}
```
### Time
O(N) -- Для сортировки используем count sort
### Memory
O(1) -- Массив фиксированного размера
### Explication
Нам даны отрезки, мы превращаем их в точки на прямой. У каждой точки есть свое значение, которое
отражает кол-во пассажиров, которые вышли или зашли в машину. Таким образом, мы проходим
по отсортированным точкам и смотрим сколько людей в машине на данный момент.

Третье решение оптимизировано для данной задачи, потому что мы знаем что значения точек от 0 до 1000, значит мы можем
применить count sort, что дает O(N) по времени и O(1) по памяти
