## Fails
### 1st try
[LOGIC] Поспешил. Решил что если первое условие не выполнилось, значит разница будет точно отрицательной. мда
```java
class Solution {
    public boolean isMonotonic(int[] nums) {
        if (nums.length < 3) {
            return true;
        }

        int lastDiff = 0;

        for (int i = 0; i < nums.length - 1; i++) { // i = 3, lastDiff = -1;
            int prev = nums[i]; // 1
            int next = nums[i + 1]; // 4

            if (prev == next) {
                continue;
            }

            int diff = next - prev; 
            if (diff > 0 && lastDiff >= 0) {
                lastDiff = diff;
                continue;
            }
            if (lastDiff <= 0) { // ERROR
                lastDiff = diff;
                continue;
            }

            return false;
        }

        return true;
    }
} 
```