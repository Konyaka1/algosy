### Solution
```java
class Solution {
    public int minimumDifference(int[] nums, int k) {
        if (k == 1) {
            return 0;
        }
        Arrays.sort(nums);

        int min = Integer.MAX_VALUE;

        for (int i = 0; i <= nums.length - k; i++) {
            int l = nums[i]; // 1
            int r = nums[i + k - 1];
            min = Math.min(min, r - l);
        }
        return min;
    }
}
```
### Time
O(n * log n) -- проходим через весь массив изначальный.
### Memory
O(log n) -- java использует quicksort для примитивов.
### Explication
Сортируем массив чтобы выборка подмассивов была самой выгодной.
Таким образом первые k элементы будут иметь минимальные значения.
Значит мы берем максимальный и минимальный из каждых k элементов и считаем их разницу.
