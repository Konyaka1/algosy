## Fails
### 1st try
[LOGIC] Поспешил. первое и второе максимальное должны быть нулями, 
а не значениями из входных данных. это ломает логику
```java
class Solution {
    public int maxProduct(int[] nums) {
        int firstMax = nums[0];
        int secondMax = nums[1];

        for (int num : nums) {
            if (num > firstMax) {
                secondMax = firstMax;
                firstMax = num;
            } else if (num > secondMax) {
                secondMax = num;
            }
        }

        return (firstMax - 1) * (secondMax - 1);
    }
}
```