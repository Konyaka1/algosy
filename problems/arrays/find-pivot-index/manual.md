### Solution
TIME: ~20min.
```java
class Solution {
    public int pivotIndex(int[] nums) {
        int leftSum = 0;
        int rightSum = 0;

        for (int i = 1; i < nums.length; i++) {
            rightSum = rightSum + nums[i];
        }

        if (leftSum == rightSum) {
            return 0;
        }

        for (int i = 1; i < nums.length; i++) {
            leftSum = leftSum + nums[i - 1];
            rightSum = rightSum - nums[i];

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
O(1) -- храним только две переменных суммы, не зависит от длины массива.
### Explication
Префиксный массив излишний. Надо мониторить только две суммы, левую и правую.
На каждой итерации мы добавляем число или отнимаем его.
```
i = 0; 0 == x[1] + x[2] + ... + x[n - 1];
i = 1; 0 + x[0] == x[2] + x[3] + ... x[n - 1];
...
i = k; 0 + x[0] + ... + x[k - 1] == x[k + 1] + x[k + 2] + ... + x[n - 1];
i = n - 1; 0 + x[0] + x[1] + ... x[n - 2] == 0
```
На каждой итерации к левой сумме добавляем `i - 1` элемент
а от правой суммы отнимаем `i` элемент и сравниваем значения сумм. 
Если равенство не было достигнуто -- возвращаем  -1.