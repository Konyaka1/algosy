### Solution
```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> secondToIndex = new HashMap<>();

        int[] result = new int[2];

        for (int i = 0; i < nums.length; i++) { // i = 1
            int requiredNum = target - nums[i]; // 2 = 9 - 7;

            Integer secondIndex = secondToIndex.get(requiredNum); // 0
            if (secondIndex != null) {
                result[0] = i;
                result[1] = secondIndex.intValue();  // [1, 0]
                break;
            } else {
                secondToIndex.put(nums[i], i); // [2 -> 0]
            }
        }

        return result;
    }
}
```

### Time
O(N) -- потому что проходим через весь массив 
### Memory
O(N) -- потому что мы храним каждый элемент и его индекс
### Explication
Используем мапу в которой храним уже подсчитанную разницу как ключ и ее индекс. В приницпе решение я бы описал подходом своего препода по проге в универе Зубовича
"Зачем считать дважды то, что уже подсчитано". Поэтому вместо двойного цикла и подсчета разницы на каждой итерации мы запоминаем уже подсчитаную разницу и индекс