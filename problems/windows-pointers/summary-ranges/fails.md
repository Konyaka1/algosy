## Fails
### 1st try
Название переменных!
```java
class Solution {

    public List<String> summaryRanges(int[] nums) {
        int left = 0;
        int right = 0;

        List<String> result = new LinkedList<>();

        while (left < nums.length) { 
            while (canMoveRight(right, nums)) {
                right = right + 1;
            }

            String res = getCurState(left, right, nums);
            
            result.add(res);

            left = right + 1;
            right = right + 1;
        }

        return result;
    }

    private boolean canMoveRight(int right, int[] nums) {
        if (right + 1 >= nums.length) {
            return false;
        }
        return nums[right + 1] - nums[right] == 1;
    }
    
    // Не обязательно использовать Integer.toString()
    // Вообще лучше стринг билдер
    private String getCurState(int left, int right, int[] nums) {
        String res = null;
        if (left == right) {
            res = Integer.toString(nums[left]);
        } else {
            res = Integer.toString(nums[left]) + "->" + Integer.toString(nums[right]);
        }
        return result; // HERE
    }
}
```
