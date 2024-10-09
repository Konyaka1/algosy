### Solution
```java
public class Solution {
    
    public int solve(String A) {
        int size = 0;
        for (char ch : A.toCharArray()) {
            if (ch == '(') {
                size++;
            } else {
                if (size == 0) {
                    return 0;
                }
                size--;
            }
        }

        if (size == 0) {
            return 1;
        } else {
            return 0;
        }
    }
}
```
### Time
O(N) -- проходим по всей строке
### Memory
O(1) -- Не используется доп память, только один int.
### Explication
Проходим по строке и эмитируем стек при помощи переменной int, которая
отражает размер стека. Найдя открытую скобку -- добавляем единицу к размеру стека.
Найди закрытую скобку -- отнимаем 1. Если же стек пустой когда мы нашли закрытую -- сразу возвращаем 0.
