## Fails

### Basic 1st try
Забыл проверить
```java
class Solution {
    public int findMaxConsecutiveOnes(int[] nums) {
        int max = 0;
        int cur = 0;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] == 1) {
                cur++;
            } else {
                if (max < cur) {
                    max = cur;
                }
                cur = 0;
            }
        }
        return max;
    }
}
```
### Sliding window 1st try
Too many errors, needs to be retried.
