### Solution
```java
class Solution {
    public int longestOnes(int[] nums, int k) {
        int l = 0;
        int r = -1;

        int maxLength = 0;
        int curState = 0;

        while (l < nums.length) {
            while (r + 1 < nums.length && this.canMove(r, curState, k, nums)) {
                r = r + 1;
                if (nums[r] == 0) {
                    curState++;
                }
            }

            maxLength = Math.max(maxLength, r - l + 1);

            if (nums[l] == 0) {
                curState--;
            }
            l = l + 1;
        }

        return maxLength;
    }

    private boolean canMove(int r, int curState, int k, int[] nums) {
        if (r + 1 >= nums.length) {
            return false;
        }
        if (nums[r + 1] == 1) {
            return true;
        }
        return curState < k;
    }
}
```
### Time
O(N) -- потому что проходим левым указателем весь массив
### Memory
O(1) -- потому что храним только фиксированное число переменные.
### Explication
Используем скользящие пересекающиеся окна, чтобы найти самую длинную последовательность.
Двигаем правый пока это единица или пока кол-во нулей позволяет.
Как только правый уперся -- двигаем левый указатель на 1 и не забываем обновить кол-во нулей если необходимо
