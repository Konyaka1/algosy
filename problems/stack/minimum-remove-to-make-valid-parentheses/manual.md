### Solution
```java
class Solution {

    public String minRemoveToMakeValid(String s) {
        int state = 0;
        int vl = 0; // valid left

        for (char ch : s.toCharArray()) {
            if (ch == '(') {
                state++;
            } else if (ch == ')' && state != 0) {
                vl++;
                state--;
            }
        }

        int vr = vl; // valid right
        StringBuilder sb = new StringBuilder(s.length());
        for (char ch : s.toCharArray()) {
            if (ch == '(') {
                if (vl > 0) {
                    // append open bracket if we can
                    sb.append(ch);
                    vl--;
                }
            } else if (ch == ')') {
                if (vl < vr) {
                    // append close bracket
                    // only if we already appended open bracket
                    sb.append(ch);
                    vr--;
                }
            } else {
                // append any other character
                sb.append(ch);
            }
        }
        return sb.toString();
    }
}
```
### Time
O(N) -- Проходим по строке два раза
### Memory
O(N) -- Для хранения строки ответа
### Explication
Проходим по строке в первый раз, чтобы посчитать кол-во валидных пар скобок. 
Если мы нашли открытую --> увеличиваем `state` на единицу. Если мы нашли закрытую, и
`state` не равен нулю, значит мы уже находили открытую скбоку, следовательно, эта пара скобок
валидна. Уменьшаем стейт на 1 и увеличиваем кол-во валидных левых скобок. 

Проходя второй раз по строке, мы знаем кол-во валидных скобок. Соответственно
в ответ добавляем открытую скобку пока можем, и добавляем закрытую, если открытых осталось меньше.
