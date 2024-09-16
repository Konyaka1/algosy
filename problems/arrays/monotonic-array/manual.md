### Solution
```java
class Solution {
    public boolean isMonotonic(int[] nums) {
        if (nums.length < 3) {
            return true;
        }

        int lastDiff = 0;

        for (int i = 0; i < nums.length - 1; i++) {
            int prev = nums[i]; 
            int next = nums[i + 1]; 

            if (prev == next) {
                continue;
            }

            int diff = next - prev; 
            if (diff > 0 && lastDiff >= 0) {
                lastDiff = diff;
                continue;
            }
            if (diff < 0 && lastDiff <= 0) {
                lastDiff = diff;
                continue;
            }

            return false;
        }

        return true;
    }
} 
```

### Time
O(N) -- потому что проходим через весь массив
### Memory
O(1) -- потому что храним только разницу между предыдущими
### Explication
Храним предыдущю разницу, которая имеет инт значение и возможны три варианта:
1) lastDiff == 0, значит что пока мы не знаем раньше было убывание или возрастание, все элементы одинаковые
2) lastDiff > 0, значит что у нас возрастание было
3) lastDiff < 0, значит что у нас убывание

На каждом шаге проверяем убывание у нас или нет, и сраниваем с lastDiff. Если совпадает, идем дальше, 
если нет то возвращаем false.

Если прошли весь цикл, то все хорошо вовзращаем true.