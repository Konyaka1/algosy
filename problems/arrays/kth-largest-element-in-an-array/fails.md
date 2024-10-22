## Fails
### 1st try
Syntax error. Forgot return statement
```java
class Solution {

    private final Random rand = new Random();

    public int findKthLargest(int[] nums, int k) {
        int indexFromEnd = nums.length - k;
        return this.quickSelect(nums, 0, nums.length, indexFromEnd);
    }

    public int quickSelect(int[] nums, int l, int r, int k) {
        int pi = this.partition(nums, l, r);

        if (pi > k) {
            this.quickSelect(nums, l, pi, k); // HERE
        } else if (pi < k) {
            this.quickSelect(nums, pi + 1, r, k); // HERE
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
            if (nums[li] < pivot) {
                li++;
            } else if (nums[ri] > pivot) {
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
### 2nd try
Logic error. Messed up if conditions
```java
class Solution {

    private final Random rand = new Random();

    public int findKthLargest(int[] nums, int k) {
        int indexFromEnd = nums.length - k;
        return this.quickSelect(nums, 0, nums.length, indexFromEnd);
    }

    public int quickSelect(int[] nums, int l, int r, int k) {
        int pi = this.partition(nums, l, r);

        if (pi < k) { // HERE
            return this.quickSelect(nums, l, pi, k);
        } else if (pi > k) { // HERE
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
            if (nums[li] < pivot) {
                li++;
            } else if (nums[ri] > pivot) {
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