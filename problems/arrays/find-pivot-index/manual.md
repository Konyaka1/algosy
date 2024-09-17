### Solution
TIME: 23:59. NOT OPTIMAL
```java
class Solution {
    public int pivotIndex(int[] nums) {
        int[] sums = new int[nums.length + 1];
        for (int i = 1; i < nums.length + 1; i++) {
            sums[i] = sums[i - 1] + nums[i - 1];
        }

        for (int i = 0; i < nums.length; i++) {
            int leftSum = sums[i];
            int rightSum = sums[nums.length] - sums[i + 1];
            if (leftSum == rightSum) {
                return i;
            }
        }

        return -1;
    }
}
```
### Time
O(N) -- проходим через весь массив изначальный.
### Memory
O(N) -- создается массив длины n + 1.
### Explication
Создаем префиксный массив и далее считаем наши суммы. `prArr[i] == x[0] + x[1] + x[i - 1]`.
Нам надо найти такое i, чтобы выполнялось условие `SUM(0, i) SUM(i + 1, N)`, то есть
`x[0] + x[1] + ... + x[i - 1] == x[i + 1] + x[i + 2] + ... + x[n - 1]`, n -- длина массива.

то есть итерируем по префиксному массиву от 0 до n, пока не найдем такое i, чтобы выполнялось условие
`prArr[i] == prArr[n] - prArr[i + 1]`, что можно записать как

`x[0] + x[1] + ... + x[i - 1] == 
(x[0] + x[1] + ... + x[n - 1]) - (x[0] + x[1] + ... + x[i]) ==
x[i + 1] + x[i + 2] + ... + x[n - 1]
`