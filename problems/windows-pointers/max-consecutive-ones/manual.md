### Solution
Basic solution
```java
class Solution {
    public int findMaxConsecutiveOnes(int[] nums) {
        int max = 0;
        int cur = 0;
        for (int num : nums) {
            if (num == 1) {
                cur++;
            } else {
                if (max < cur) {
                    max = cur;
                }
                cur = 0;
            }
        }
        if (max < cur) {
            max = cur;
        }
        return max;
    }
}
```
Sliding window solution
```java
class Solution {
    public int findMaxConsecutiveOnes(int[] nums) {
        int l = 0;
        int r = 0;

        int max = 0;
        while (l < nums.length) {
            while (r + 1 < nums.length && nums[r + 1] == nums[r]) {
                r = r + 1;
            }

            if (nums[r] == 1) {
                max = Math.max(r - l + 1, max);
            }

            l = r + 1;
            r = r + 1;
        }

        return max;
    }
}
```
### Time
Basic: O(N) -- проходим по всем элементам массива
Sliding window: O(N) -- проходим по всем элементам массива
### Memory
Basic: O(1) -- нет доп памяти, только счетчик и макс счетчик
Sliding window: O(1) -- нет доп памяти, только макс счетчик и указатели
### Explication
В обычном решении идея проста -- проходим по массиву, если нашли единицу, то увеличили счетчик,
если нашли ноль -- обновили максимум и обнулили счетчик. Не забыть сделать то же самое, при выходе
из цикла.

В плавающем окне используем технику не пересекающихся окон, ищем все окна одних и тех же элементов,
то есть окна с нулями и окна с единицами и обновляем счетчик, если окно состоит из единиц.
