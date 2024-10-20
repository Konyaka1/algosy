### Solution 1
From bottom to top
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
### Solution 2
From top to bottom, recursive
```java
class Solution {
    public int[] sortArray(int[] nums) {
      
        return sortArray(nums, 0, nums.length);
    }
    
    private int[] sortArray(int[] nums, int l, int r) {
        if (r - l < 2) {
            return new int[]{nums[l]};
        } 
        int middle = (l + r) / 2;
        
        int[] left = sortArray(nums, l, middle);
        int[] right = sortArray(nums, middle, r);
        
        return mergeSorted(left, right);
    }

    private int[] mergeSorted(int[] left, int[] right) {
        int[] res = new int[left.length + right.length];
        
        int i1 = 0;
        int i2 = 0;
        
        int i = 0;
        
        while (i1 < left.length && i2 < right.length) {
            if (left[i1] < right[i2]) {
                res[i++] = left[i1++];
            } else if (left[i1] > right[i2]) {
                res[i++] = right[i2++];
            } else {
                res[i++] = left[i1++];
                res[i++] = right[i2++];
            }
        }
        
        while (i1 < left.length) {
            res[i++] = left[i1++];
        }
        
        while (i2 < right.length) {
            res[i++] = right[i2++];
        }

        return res;
    }
}
```
### Time
O(N * log N) -- потому что делаем logN итераций для сортировки под массивов
### Memory
O(N) -- для хранения доп массива
### Explication
Начинаем рекурсивно сортировать половины массивов, а затем применять мерж сорт
для сортированных половин. При под массиве длины 1 возвращаем один элемент как массив. 
И рекурсия начинает раскручиваться обратно.
