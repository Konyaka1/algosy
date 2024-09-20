### Solution
TIME: ~23min.
```java
class Solution {
    public int subarraySum(int[] nums, int k) {  
        Map<Integer, Integer> groupedSums = new HashMap<>();
        groupedSums.put(0, 1); 

        int currentSum = 0;
        int result = 0;
        for (int num : nums) {
            currentSum = currentSum + num;  

            int target = currentSum - k; 

            result = result + groupedSums.getOrDefault(target, 0);  

            groupedSums.merge(currentSum, 1, Integer::sum);
        }

        return result;
    }
}
```
### Time
O(N) -- проходим через весь массив один раз, в цикле операции за O(1).
### Memory
O(N) -- храним каждую префиксную сумму
### Explication
Идея скрыта за следующей идеей. Нам надо найти все под суммы, равные k.
```
sum(l, r) == k where l <= r
sum(l, r) == sum(0, r) - sum(0, l).
sum(0, r) - sum(0, l) == k

sum(0, r) - k = sum(0, l)
```
Нам надо перебрать все r и все возможные l. Чтобы ускорить это, нам надо сохранять предыдущие значения.
Предыдущие значения это `sum(0, l)`. Каждую итерацию мы считаем следующую сумму от 0 до r.
Поскольку нас не интересуют индексы l и r, то мы можем сохранить в мапу только значение этой суммы.
То есть если в мапу хранится [5 -> 3], это значит что есть `l1, l2, l3` такие что:
```
sum(0, l1) == sum(0, l2) == sum(0, l3) == 5
```
То есть отнимая `k` от `sum(0, r)` мы находим какую-то сумму `sum(0, l)`.
Остается проверить, сколько у нас было сохранено уже предыдущих сумм с таким значением.

Example:
```
we know that answer has x3 + x4, and x1 + x2 + x3 + x4. so their sum equals to k

in map we have
sum1 -> 2 ([x0], [x0 + x1 + x2])
sum2 -> 1 ([x0 + x1])

on the 4 iteration we kn0w sum of 0 to 4 we know x0 + x1 + x2 + x3 + x4.

sum(0, r) - k == sum(0, l); using this formula

x0 + x1 + x2 + x3 + x4 - k = x3 + x4 OR x1 + x2 + x3 + x4.

we know k might be x1 + x2 + x3 + x4 OR x3 + x4

so (x0 + x1 + x2 + x3 + x4) - (x1 + x2 + x3 + x4) == x0 == sum1 -- first value in map
OR 
so (x0 + x1 + x2 + x3 + x4) - (x3 + x4) == x0 + x1 + x2 == sum1 -- first value in map

by calculating sum(0,4) we found two pairs so we add 2 to result count.
```