### Solution
```java
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        int left = 0;
        int right = numbers.length - 1;

        while (left < right) {
            int curSum = numbers[left] + numbers[right];

            if (curSum > target) {
                right--;
            } else if (curSum < target) {
                left++;
            } else {
                return new int[]{left + 1, right + 1};
            }
        }

        return new int[]{-1, -1};
    }
}
```
### Time
O(N) -- потому что проходим по всему массиву
### Memory
O(1) -- потому что храним только два указателя и сумму
### Explication
Мы знаем что слева самое маленькое число и справа самое большое.
Их сумма равна числу `x1`. Если мы возьмем второе самое маленькое число
и сложим его с самым большим, мы получим сумма `x2`, которая больше чем `x1`.
Аналогично мы получим сумму `x3`, сложив самое маленькое и второе самое большое,
при этом `x3` будет меньше `x1`.

Таким образом, передвигая одно слагаемое, мы можем считать текущую сумму и найти
сумму равную `target`. 
