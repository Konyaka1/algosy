## Fails
### 1st try
Забываю поставить скобки типу массив
```java
class Solution {
    public int[] sortedSquares(int[] nums) {
        int left = 0;
        int right = nums.length - 1;  

        int resId = nums.length - 1;  
        int result = new int[nums.length];   // HERE

        while (resId >= 0) {  
            int leftSq = nums[left] * nums[left];  
            int rightSq = nums[right] * nums[right];  

            if (leftSq < rightSq) {  
                result[resId] = rightSq;
                right--;
            } else {
                result[resId] = leftSq;
                left++;
            }

            resId--;
        }

        return result;
    }
}
```