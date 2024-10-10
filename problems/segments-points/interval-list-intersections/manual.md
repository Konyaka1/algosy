### Solution
```java
class Solution {
    public int[][] intervalIntersection(int[][] firstList, int[][] secondList) {
        List<int[]> res = new ArrayList<>();

        int fp = 0;
        int sp = 0;

        while (fp < firstList.length && sp < secondList.length) {
            int[] fdot = firstList[fp];
            int[] sdot = secondList[sp]; 

            int max = Math.max(fdot[0], sdot[0]); 
            int min = Math.min(fdot[1], sdot[1]); 
            if (max <= min) {
                int[] dot = new int[]{max, min}; 
                res.add(dot);
            }

            if (fdot[1] <= sdot[1]) {
                fp++;
            } else {
                sp++;
            }
        }

        return res.toArray(new int[0][]);
    }
}
```
### Time
O(N + M) -- проходим по двум спискам, в худшем случае пройдем по двум до конца 
### Memory
O(N + M) -- в худшем случае в ответе будет лежать все возможные пересечения
### Explication
Проходим по двум спискам и проверяем пересекаются ли текущие точки. Если да --
добавляем пересечение в результат. Далее главное решить какую точку взять следующую.
Для этого мы смотрим какой из концов отрезков меньше. Тот что меньше мы двигаем. Если первый
меньше -- двигаем первый указатель.
