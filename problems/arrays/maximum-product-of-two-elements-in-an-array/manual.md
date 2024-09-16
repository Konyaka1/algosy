### Solution
```java
 class Solution {
    public int maxProduct(int[] nums) {
        int firstMax = 0;
        int secondMax = 0;

        for (int num : nums) {
            if (num > firstMax) {
                secondMax = firstMax;
                firstMax = num;
            } else if (num > secondMax) {
                secondMax = num;
            }
        }

        return (firstMax - 1) * (secondMax - 1);
    }
}
```

### Time
O(N) -- потому что проходим через весь массив
### Memory
O(1) -- потому что храним только два числа
### Explication
Проходим через весь массив и ищем максимальный элемент, есть два сценария:
1) Если текущий больше чем первый максимум, обновляем второй максимум значением первого максимума
и обновляем первый максимум текущим.
2) Иначе проверяем, больше ли текущий элемент, чем второй максимум. если больше то обновляем второй максимум