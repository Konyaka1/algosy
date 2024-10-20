### Solution
```java
class Solution {
    public int[] sortArray(int[] nums) {
        int[] tmpResult = new int[nums.length];

        for (int size = 1; size < nums.length; size = size * 2) {
            for (int i = 0; i < nums.length; i = i + size * 2) {
                int r1 = Math.min(nums.length, i + size);
                int r2 = Math.min(nums.length, r1 + size);
                mergeSorted(tmpResult, nums, i, r1, r2);
            }
            System.arraycopy(tmpResult, 0, nums, 0, nums.length);
        }

        return nums;
    }

    private void mergeSorted(int[] result, int[] nums, int l1, int middle, int r2) {
        int i1 = l1;
        int i2 = middle;

        int res = l1;

        while (i1 < middle && i2 < r2) {
            if (nums[i1] < nums[i2]) {
                result[res++] = nums[i1++];
            } else if (nums[i1] > nums[i2]) {
                result[res++] = nums[i2++];
            } else {
                result[res++] = nums[i1++];
                result[res++] = nums[i2++];
            }
        }

        while (i1 < middle) {
            result[res++] = nums[i1++];
        }

        while (i2 < r2) {
            result[res++] = nums[i2++];
        }
    }
}
```
### Time
O(N * log N) -- потому что делаем logN итераций для сортировки под массивов
### Memory
O(N) -- для хранения доп массива
### Explication
Мы знаем, что под массив длины 1 уже отсортирован, 
поэтому мы начинаем сортировать под массивы длины 2, 4, 8 ... и так далее. 
Для сортировки надо использовать доп массив в который мы записываем результаты.
Важно: после каждой сортировки определенной длины надо перенести результат в изначальный массив.
