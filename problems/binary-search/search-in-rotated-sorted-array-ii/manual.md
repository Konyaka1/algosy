### Solution
```java
class Solution {
    public boolean search(int[] nums, int target) {
        int l = 0;
        int r = nums.length;

        while (r > 1 && nums[0] == nums[r - 1]) {
            r--;
        }

        // looking for pivot
        while (r - l > 1) {
            int m = (l + r) / 2;

            if (nums[m] >= nums[l]) {
                l = m;
            } else {
                r = m;
            }
        }
        // l points to pivot.

        if (target < nums[0]) {
            if (l == nums.length - 1) {
                return false;
            }
            return this.binSearch(l + 1, nums.length, nums, target);
        } else {
            return this.binSearch(0, l + 1, nums, target);
        }
    }

    private boolean binSearch(int l, int r, int[] nums, int target) {
        while (r - l > 1) {
            int m = (l + r) / 2;

            if (nums[m] <= target) {
                l = m;
            } else {
                r = m;
            }
        }

        return nums[l] == target;
    }
}
```
### Time
O(log N) avg, O(N) худшее 
### Memory
O(1) -- используется константная память
### Explication

