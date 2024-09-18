## Fails
### 1st try
[logic | wa] Неправильный ответ для случая, когда k == 1. Нужно найти разницу, а не минимальное значение.
```java
class Solution {
    public int minimumDifference(int[] nums, int k) {
        if (k == 1) {
            int min = nums[0];
            for (int num : nums) {
                min = Math.min(num, min);
            }
            return min;
        }
        int max1 = Integer.MIN_VALUE; // MAX
        int max2 = Integer.MIN_VALUE; // MAX

        int min1 = Integer.MAX_VALUE; // MIN
        int min2 = Integer.MAX_VALUE; // MIN

        for (int num : nums) { // 7
            if (num > max1) { // 7 > 9
                max2 = max1; // max2 = 7
                max1 = num; // max1 = 9
            } else {
                max2 = Math.max(num, max2); // max2 = 7
            }

            if (num < min1) { // 7 < 4
                min2 = min1; // min2 = 4
                min1 = num; // min1 = 1
            } else {
                min2 = Math.min(min2, num); // min2 = 4
            }
        }

        return Math.min(max1 - max2, min2 - min1);
    }
}
```
### 2nd try
[logic | wa] Неправильный ответ для случая [87063,61094,44530,21297,95857,93551,9918] и k = 6.
Да и в принципе неправильный подход к задаче
```java
class Solution {
    public int minimumDifference(int[] nums, int k) {
        if (k == 1) {
            return 0;
        }
        int max1 = Integer.MIN_VALUE; // MAX
        int max2 = Integer.MIN_VALUE; // MAX

        int min1 = Integer.MAX_VALUE; // MIN
        int min2 = Integer.MAX_VALUE; // MIN

        for (int num : nums) { // 7
            if (num > max1) { // 7 > 9
                max2 = max1; // max2 = 7
                max1 = num; // max1 = 9
            } else {
                max2 = Math.max(num, max2); // max2 = 7
            }

            if (num < min1) { // 7 < 4
                min2 = min1; // min2 = 4
                min1 = num; // min1 = 1
            } else {
                min2 = Math.min(min2, num); // min2 = 4
            }
        }

        return Math.min(max1 - max2, min2 - min1);
    }
}
```