## Fails
Always use new variables names. Easy to forget that name is already defined
```java
class Solution {
    public void rotate(int[] nums, int k) {
            int k = k % nums.length; // HERE
            
            rotate(nums, 0, nums.length - k - 1);
            rotate(nums, nums.length - k, nums.length - 1);
            rotate(nums, 0, nums.length - 1);
    }
    
    private void rotate(int[] nums, int l, int r) {
        while (l < r) {
            int tmp = nums[r];
            nums[r] = nums[l];
            nums[l] = tmp;
            l++;
            r--;
        }
    }
}
```