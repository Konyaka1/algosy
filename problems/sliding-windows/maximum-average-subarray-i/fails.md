## Fails
### 1st try
Нужно делить на k, а не на 4.
```java
class Solution {
    public double findMaxAverage(int[] nums, int k) {
        int curSum = 0;

        for (int i = 0; i < k; i++) {
            curSum += nums[i];
        }

        int maxSum = curSum;
        
        
        for (int i = k; i < nums.length; i++) {
            curSum = curSum + nums[i] - nums[i - k];
            maxSum = Math.max(maxSum, curSum);
        }

        return maxSum / 4.0;
    }
}
```