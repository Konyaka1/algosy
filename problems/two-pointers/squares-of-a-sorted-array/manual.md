### Solution
```java
class Solution {
    public int[] sortedSquares(int[] nums) {
        int left = 0;
        int right = nums.length - 1; 

        int resId = nums.length - 1;  
        int[] result = new int[nums.length];  

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

### Time
O(N) -- потому что проходим по всему массиву
### Memory
O(N) -- потому что надо хранить результат
### Explication
Чтобы однозначно сказать, чей квадрат для чисел `x1` и `x2` больше
надо сравнить их модули, или сами квадраты. Мы знаем что самый левый
и самый правый элемент в общем случае будут иметь максимальный модуль,
потому что слева хранится самое минимальное число (которое может быть
отрицательным, что и делает его модуль большим) и справа самое больше число.

Идея в том, чтобы взять два указателя слева и справа, и считать квадраты -- наибольший
записывать в конец результирующего массива, указатель наибольшего сдвигать в сторону середины
(делать ++ для левого, и -- для правого)
