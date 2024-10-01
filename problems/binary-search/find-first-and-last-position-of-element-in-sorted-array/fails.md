## Fails
### 1try
Syntax. we can't return {}.
```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
        int l = -1;
        int r = nums.length - 1;
        
        while (r - l > 1) {
            int m = (l + r) / 2;
            if (this.isStrictLess(nums[m], target)) {
                l = m;
            } else {
                r = m;
            }
        }
        if (nums[r] != target) {
            // HERE
            return {-1,-1};
        }
        int leftAnswer = r;
        
        l = r;
        r = nums.length;
        
        while (r - l > 1) {
            int m = (l + r) / 2;
            if (this.isLessOrEqual(nums[m], target)) {
                l = m;
            } else {
                r = m;
            }
        }
        
        // HERE
        return {leftAnswer, l};
    }
    
    private boolean isStrictLess(int xi, int target) {
        return xi < target;
    }
    
    private boolean isLessOrEqual(int xi, int target) {
        return xi <= target;
    }
}
```
### 2nd try
Syntax. We don't need to provide length for in place array creation
```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
        int l = -1;
        int r = nums.length - 1;
        
        while (r - l > 1) {
            int m = (l + r) / 2;
            if (this.isStrictLess(nums[m], target)) {
                l = m;
            } else {
                r = m;
            }
        }
        if (nums[r] != target) {
            // HERE
            return new int[2]{-1,-1};
        }
        int leftAnswer = r;
        
        l = r;
        r = nums.length;
        
        while (r - l > 1) {
            int m = (l + r) / 2;
            if (this.isLessOrEqual(nums[m], target)) {
                l = m;
            } else {
                r = m;
            }
        }
        // HERE
        return new int[2]{leftAnswer, l};
    }
    
    private boolean isStrictLess(int xi, int target) {
        return xi < target;
    }
    
    private boolean isLessOrEqual(int xi, int target) {
        return xi <= target;
    }
}
```
### 3rd try
Wrong Answer. Didn't handle corner case. empty array.
```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
        int l = -1;
        int r = nums.length - 1;
        
        while (r - l > 1) {
            int m = (l + r) / 2;
            if (this.isStrictLess(nums[m], target)) {
                l = m;
            } else {
                r = m;
            }
        }
        if (nums[r] != target) {
            return new int[]{-1,-1};
        }
        int leftAnswer = r;
        
        l = r;
        r = nums.length;
        
        while (r - l > 1) {
            int m = (l + r) / 2;
            if (this.isLessOrEqual(nums[m], target)) {
                l = m;
            } else {
                r = m;
            }
        }
        
        return new int[]{leftAnswer, l};
    }
    
    private boolean isStrictLess(int xi, int target) {
        return xi < target;
    }
    
    private boolean isLessOrEqual(int xi, int target) {
        return xi <= target;
    }
}
```