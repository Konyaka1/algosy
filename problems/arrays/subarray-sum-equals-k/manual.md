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
