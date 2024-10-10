### Solution
Intervals method
```java
class Solution {
    public int findMinArrowShots(int[][] points) {
        Comparator<int[]> comp = (a, b) -> Integer.compare(a[0], b[0]);
        Arrays.sort(points, comp);

        int res = 1;
        int[] top = new int[] {points[0][0], points[0][1]};

        for (int i = 1; i < points.length; i++) {
            int left = Math.max(top[0], points[i][0]);
            int right = Math.min(top[1], points[i][1]);
            if (left <= right) {
                top[0] = left;
                top[1] = right;
            } else {
                top[0] = points[i][0];
                top[1] = points[i][1];

                res = res + 1;
            }
        }

        return res;
    }
}
```
### Time
O(N log N) -- потому что 
### Memory
O(1) -- потому что не используется доп память
### Explication
Сортируем точки по первой позиции. Далее начинаем мержить интервалы, ответом будет
кол-во замерженных интервалов. По скольку нам надо вернуть только кол-во, будем хранить
только последний посчитанный интервал. Для этого храним `int[] top` и `int res`. 
Top хранит последний замерженный участок. Важно, что Top хранит пересечение, а не объединение, 
потому что для случая `[1, 3], [3, 4], [4, 5]` результатом является две стрелы, а результат
мержинга даст один отрезок. Поэтому каждый мержинг мы сужаем "поиск".