### Solution
```java
class Solution {
    public void moveZeroes(int[] nums) {
        int fast = 0;
        int slow = 0;

        while (fast < nums.length) {
            if (nums[fast] == 0) {
                fast++;
            } else {
                nums[slow] = nums[fast];
                slow++;
                fast++;
            }
        }

        while (slow < nums.length) {
            nums[slow] = 0;
            slow++;
        }
    }
}
```

### Time
O(N) -- потому что проходим по всему массиву
### Memory
O(1) -- независимо от длины массива мы храним только два указателя.
### Explication
Создаем два указателя. Один ищет ненулевые элементы, другой является индексом
_ненулевых элементов_ в результирующем массиве. `fast >= slow` всегда, поэтому мы не боимся
перезаписи элементов или записи в неправильном порядке
