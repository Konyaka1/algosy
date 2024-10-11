### Solution

```java
import java.util.function.IntPredicate;

class Solution {
    public int search(int[] nums, int target) {
        IntPredicate rotation = (x) -> x >= nums[0];

        int lastRotated = this.binSearch(nums, rotation, 0, nums.length);

        IntPredicate findTarget = (x) -> x <= target;

        int l;
        if (target < nums[0]) {
            if (lastRotated == nums.length - 1) {
                return -1;
            }
            l = this.binSearch(nums, findTarget, lastRotated + 1, nums.length);
        } else {
            l = this.binSearch(nums, findTarget, 0, lastRotated + 1);
        }
        return nums[l] == target ? l : -1;
    }

    private int binSearch(int[] nums, IntPredicate test, int l, int r) {
        while (r - l > 1) {
            int m = (r + l) / 2;
            if (test.test(nums[m])) {
                l = m;
            } else {
                r = m;
            }
        }

        return l;
    }
}
```
### Time
O(log N) -- постоянно делим массив на 2
### Memory
O(1) -- Не используется доп память
### Explication
Делаем бинарный поиск с условием, что элемент должен быть больше первого, таким образом мы найдем
место, где элементы были rotated. 
```text
function: x[i] >= x[0]
 g  g  g  g  f  f  f
[4, 5, 6, 7, 0, 1, 2]     
          l  r 
          
 g  g  g  g  g  g  g
[0, 1, 2, 4, 5, 6, 7]      l == length - 1 --> значит все элементы отсортированы
                   l  r
                   
                             
 g  f  f  f  f  f  f
[8, 1, 2, 4, 5, 6, 7]     
 l  r
```
Таким образом l указывает на наибольший элемент, а r на наименьший (за исключением второго 
случая когда все элементы отсортированы)

Вторым действием мы смотрим, в какой части массива нам делать бинарный поиск. Если таргет меньше первого элемента,
то мы ищем в правой части массива, то есть делаем поиск по `[l + 1, arr.length]`. **Attention**: если все элементы 
отсортированы и таргет меньше первого, то поиск можно и не делать, а вернуть -1 сразу.

Если же таргет больше либо равен первому числу, то мы делаем поиск по первой части массива `[0, l + 1]`.
