### Solution
```java
class Solution {

    public int[] addTwoNumbers(int[] arr1, int[] arr2) {
        int maxLength = Math.max(arr1.length, arr2.length); // 3

        int[] result = new int[maxLength + 1]; // [0, 0, 0, 0]

        int ai = arr1.length - 1; // 2
        int bi = arr2.length - 1; // 0

        int addition = 0;
        for (int i = 0; i < maxLength; i++) { // i = 2 < 3
            int numberA = ai - i >= 0 ? arr1[ai - i] : 0; // a[0] = 9
            int numberB = bi - i >= 0 ? arr2[bi - i] : 0; // b[-1] = 0

            int currSum = numberA + numberB + addition; // 10 = 9 + 0 + 1

            if (currSum >= 10) {
                addition = 1;
                currSum = currSum % 10;
            } else {
                addition = 0;
            }

            result[maxLength - i] = currSum;
        }

        if (addition == 1) {
            result[0] = 1;
        }

        return result;
    }
}
```

### Time
O(N) -- Проходим через каждый элемент массива и складываем их
### Memory
O(N) -- Размер массива для ответа
### Explication
Для ответа создаем массив из максимальной длины + 1. Создаем два указателя для 
итерирования через каждый массив. Если индекс меньше нуля -- ставим значение в 0.
Итерируем от нуля до макс длины. 0 указывает нулевой разряд. Складываем и сохраняем в результирующий массив.
Также надо учесть случай, когда мы вышли из цикла, но еще осталась единица в addition.