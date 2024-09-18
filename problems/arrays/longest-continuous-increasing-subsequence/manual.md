### Solution
TIME: 7:33.
```java
class Solution {
    public int findLengthOfLCIS(int[] nums) {
        int maxLength = 1;
        int prev = nums[0]; 
        int curLength = 1;
        for (int i = 1; i < nums.length; i++) {
            int next = nums[i];
            if (prev < next) {
                curLength++;
            } else {
                maxLength = Math.max(curLength, maxLength);
                curLength = 1;
            }
            prev = next;
        }

        return Math.max(curLength, maxLength);
    }
}
```
### Time
O(N) -- проходим через весь массив изначальный.
### Memory
O(1) -- используем фикс кол-во переменных вне зависимости от длины массива.
### Explication
Итерируем массив и проверяем предыдущий и текущий. 
Если возрастание, то прибавляем к текущей длине 1.
Важно, что текущая длина всегда равна 1, потому что предыдущий элемент либо сам является 
НВП, либо является частью НВП. НВП -- непрерывно возрастающая последовательность.

