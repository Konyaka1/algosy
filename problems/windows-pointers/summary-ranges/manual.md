### Solution
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

    private String getCurState(int left, int right, int[] nums) {
        StringBuilder sb = new StringBuilder();
        sb.append(nums[left]);

        if (left != right) {
            sb.append("->");
            sb.append(nums[right]);
        }

        return sb.toString();
    }
}
```
### Time
O(N) -- проходим по всему массиву один раз
### Memory
O(1) -- не используем доп память зависящую от длины массива (не считаем память нужную для ответа)
### Explication
Проходим по массиву с левым и правым указателем. Проходим до тех пор, пока левый не будет больше массива.

**ВАЖНО**: Перед тем как переместить правый, мы должны убедиться, что это можно сделать. Таким образом мы всегда имеет 
строго левый указывает на начало, а правый на конец _включительно_

### Note
`StringBuilder` имеет перегрузки для всех типов, по этому туда можно спокойно передавать инты.
