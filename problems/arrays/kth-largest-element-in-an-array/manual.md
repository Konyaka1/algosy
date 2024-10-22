### Solution
```java
class Solution {

    private final Random rand = new Random();

    public int findKthLargest(int[] nums, int k) {
        return this.quickSelect(nums, 0, nums.length, k - 1);
    }

    public int quickSelect(int[] nums, int l, int r, int k) {
        int pi = this.partition(nums, l, r);

        if (pi > k) {
            return this.quickSelect(nums, l, pi, k);
        } else if (pi < k) {
            return this.quickSelect(nums, pi + 1, r, k);
        } else {
            return nums[pi];
        }
    }

    public int partition(int[] nums, int l, int r) {
        int randIndex = this.rand.nextInt(r - l) + l;
        int pivot = nums[randIndex];

        swap(nums, randIndex, l);

        int li = l + 1;
        int ri = r - 1;

        while (li <= ri) {
            if (nums[li] > pivot) {
                li++;
            } else if (nums[ri] < pivot) {
                ri--;
            } else {
                swap(nums, li, ri);
                li++;
                ri--;
            }
        }
        swap(nums, l, ri);

        return ri;
    }

    public void swap(int[] nums, int l, int r) {
        int tmp = nums[r];
        nums[r] = nums[l];
        nums[l] = tmp;
    }
}
```
### Time
O(N) avg, O(N^2) worst 
### Memory
O(log N) -- потому что рекурсивные вызовы
### Explication
Выполняем реализацию quick sort, но только для части массива. Это значит,
что мы совершаем итерацию quick sort, а затем проверяем на каком месте наш pivot. 
Нам нужно выполнять следующую итерацию quick sort для левой или правой части массива.
