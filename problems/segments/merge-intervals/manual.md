### Solution
```java
class Solution {
    public int[][] merge(int[][] intervals) {
        Comparator<int[]> comp = (a, b) -> a[0] - b[0];

        Arrays.sort(intervals, comp);

        List<int[]> res = new ArrayList<>(intervals.length);
        res.add(intervals[0]);

        for (int i = 1; i < intervals.length; i++) {
            int[] last = res.get(res.size() - 1);
            if (this.isIntersected(last, intervals[i])) {
                this.merge(last, intervals[i]);
            } else {
                res.add(intervals[i]);
            }
        }

        return res.toArray(new int[0][]);
    }

    private boolean isIntersected(int[] a, int[] b) {
        return Math.max(a[0], b[0]) <= Math.min(a[1], b[1]);
    }

    private void merge(int[] a, int[] b) {
        a[0] = Math.min(a[0], b[0]);
        a[1] = Math.max(a[1], b[1]);
    }
}
```
### Time
O(N log N) -- сортировка массива + прохождение по всему массиву
### Memory
O(N) -- Для сортировки память не нужна, но память нужна для прохождения массива
### Explication
Сортируем точки. Затем проходим по одной и проверяем пересекаются ли они с последней точкой в ответе.
Если да -- мержим, иначе добавляем текущую в ответ. 
