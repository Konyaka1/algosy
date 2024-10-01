### Solution
```java
class Solution {
    public double findMaxAverage(int[] nums, int k) {
        int curSum = 0;

        for (int i = 0; i < k; i++) {
            curSum += nums[i];
        }

        int maxSum = curSum;


        for (int i = k; i < nums.length; i++) {
            curSum = curSum + nums[i] - nums[i - k];
            maxSum = Math.max(maxSum, curSum);
        }

        return maxSum / (double) k;
    }
}
```
### Time
O(N) -- потому что проходим левым указателем весь массив
### Memory
O(1) -- потому что храним только фиксированное число переменные.
### Explication
Проходим по массиву и собираем текущую сумму. Важно -- при делении надо привести k к double,
иначе результат будет int.
