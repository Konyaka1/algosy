### Solution
```java
class Solution {
    public int longestSubarray(int[] nums) {
        int l = 0;
        int r = -1;

        int maxLength = 0;
        boolean hasZero = false;

        while (l < nums.length) {
            while (this.canMove(r, hasZero, nums)) {
                r = r + 1;
                if (nums[r] == 0) {
                    hasZero = true;
                }
            }

            maxLength = Math.max(maxLength, r - l);

            if (r + 1 == nums.length) {
                break;
            }

            if (nums[l] == 0) {
                hasZero = false;
            }
            l = l + 1;
        }

        return maxLength;
    }

    private boolean canMove(int r, boolean hasZero, int[] nums) {
        if (r + 1 >= nums.length) {
            return false;
        }
        if (nums[r + 1] == 1) {
            return true;
        }
        // we know r + 1 is zero
        return !hasZero;
    }
}
```
### Time
O(N) -- потому что проходим левым указателем весь массив
### Memory
O(1) -- потому что храним только фиксированное число переменных.
### Explication
Используем скользящие пересекающиеся окна, чтобы найти самую длинную последовательность.
Двигаем правый пока это единица или если это первый ноль.
Как только правый уперся -- двигаем левый указатель на 1 и не забываем обновить кол-во нулей если необходимо.
