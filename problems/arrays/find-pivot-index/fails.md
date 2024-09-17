## Fails
### 1st try
Забыл поставить `[]` для sums.
```java
class Solution {
    public int pivotIndex(int[] nums) {
        int sums = new int[nums.length + 1];
        for (int i = 1; i < nums.length + 1; i++) {
            sums[i] = sums[i - 1] + nums[i - 1];
        }

        for (int i = 0; i < nums.length; i++) {
            int leftSum = sums[i];
            int rightSum = sums[nums.length] - sums[i + 1];
            if (leftSum == rightSum) {
                return i;
            }
        }

        return -1;
    }
}
```
NOT OPTIMAL SOLUTION