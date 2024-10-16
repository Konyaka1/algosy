### Recursive solution
```java
class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> res = new ArrayList<>();
        char[] buffer = new char[n * 2];

        this.iterate(0, 0, buffer, res);

        return res;
    }

    public void iterate(int curLeft, int curRight, char[] buffer, List<String> res) {
        int curDepth = curLeft + curRight;
        if (curDepth == buffer.length) {
            res.add(new String(buffer));
            return;
        }
        if (curLeft == curRight) {
            buffer[curDepth] = '(';
            iterate(curLeft + 1, curRight, buffer, res);
        } else if (curLeft == buffer.length / 2) {
            buffer[curDepth] = ')';
            iterate(curLeft, curRight + 1, buffer, res);
        } else {
            buffer[curDepth] = '(';
            iterate(curLeft + 1, curRight, buffer, res);

            buffer[curDepth] = ')';
            iterate(curLeft, curRight + 1, buffer, res);
        }
    }
}
```
### Time
O(Cn) -- число Каталана
### Memory
O(Cn) -- число Каталана
### Explication
Рекурсивно опускаемся вниз зная предыдущий результат. На каждой итерации
проверяем кол-во открытых и закрытых скобок. Как только кол-во открытых равно кол-во закрытых --
мы не можем больше добавить закрытой скобки, поэтому добавляем только открытую. Как только
кол-во открытых равно половине длины -- значит открытые скобки закончились, добавляем только закрытые скобки.
В любой другом случае итерируем вниз с двумя вариантами, обновляя кол-во открытых и закрытых.
