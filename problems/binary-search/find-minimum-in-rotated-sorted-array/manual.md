### Solution
```java
class Solution {
    public int findMin(int[] nums) {
        int l = 0;
        int r = nums.length;

        while (r - l > 1) {
            int m = l + (r - l) / 2;

            if (nums[m] >= nums[0]) {
                l = m;
            } else {
                r = m;
            }
        }

        if (l == nums.length - 1) {
            return nums[0];
        } else {
            return nums[l + 1];
        }
    }
}
```
### Time
O(log N) -- делаем бинарный поиск
### Memory
O(1) -- не используется доп память
### Explication
Бинарным поиском делим элементы на большие чем нулевой элемент и на меньшие.
Таким образом левый будет стоять на элементах больших, а правый на меньших.
Следовательно, ответ находится в следующем от `l` месте. 
**Attention**: левый может указывать на конец массива, поэтому надо вернуть нулевой

