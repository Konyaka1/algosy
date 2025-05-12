### Solution
```go
func twoSum(nums []int, target int) []int {
    valID := make(map[int]int)
    
    for id, val := range nums {
        if firstID, ok := valID[val]; ok {
            return []int{firstID, id}
        } else {
            requiredNum := target - val
            valID[requiredNum] = id
        }
    }
    
    return []int{-1, -1}
}
```
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
### Note
#### Syntax improvements
In java we can return array in following way
```java
public int[] getArray() {
    Integer first = 234;
    int second = 25;
    char third = 'a';
    return new int[]{first, second, third, 0};
}
```