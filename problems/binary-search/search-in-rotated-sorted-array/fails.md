## Fails
### 1st try
Неправильно написана функция проверки для нахождения `target`.
```java
class Solution {
    public int search(int[] nums, int target) {
        Comparison rotation = (x) -> x >= nums[0];

        int lastRotated = this.binSearch(nums, rotation, 0, nums.length);
        
        // HERE
        Comparison findTarget = (x) -> x >= nums[0];

        int l = 0;
        if (target < nums[0]) {
            // all sorted
            if (lastRotated == nums.length - 1) {
                return -1;
            }
            // bin search in right part.
            l = this.binSearch(nums, findTarget, lastRotated + 1, nums.length);
        } else {
            // bin search in left part.
            l = this.binSearch(nums, findTarget, 0, lastRotated + 1);
        }
        return nums[l] == target ? l : -1;
    }

    interface Comparison {
        boolean test(int x);
    }

    private int binSearch(int[] nums, Comparison test, int l, int r) {
        while (r - l > 1) {
            int m = (r + l) / 2;
            if (test.test(nums[m])) {
                l = m;
            } else {
                r = m;
            }
        }

        return l;
    }
}
```
### 2nd try
Неправильно написана функция проверки для нахождения `target`.
```java
class Solution {
    public int search(int[] nums, int target) {
        Comparison rotation = (x) -> x >= nums[0];

        int lastRotated = this.binSearch(nums, rotation, 0, nums.length);
        // HERE
        Comparison findTarget = (x) -> x <= nums[0];

        int l = 0;
        if (target < nums[0]) {
            // all sorted
            if (lastRotated == nums.length - 1) {
                return -1;
            }
            // bin search in right part.
            l = this.binSearch(nums, findTarget, lastRotated + 1, nums.length);
        } else {
            // bin search in left part.
            l = this.binSearch(nums, findTarget, 0, lastRotated + 1);
        }
        return nums[l] == target ? l : -1;
    }

    interface Comparison {
        boolean test(int x);
    }

    private int binSearch(int[] nums, Comparison test, int l, int r) {
        while (r - l > 1) {
            int m = (r + l) / 2;
            if (test.test(nums[m])) {
                l = m;
            } else {
                r = m;
            }
        }

        return l;
    }
}
```