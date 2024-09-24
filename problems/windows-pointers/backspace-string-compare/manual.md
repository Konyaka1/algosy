### Solution
```java
class Solution {
    public boolean backspaceCompare(String s, String t) {
        int si = s.length() - 1;
        int ti = t.length() - 1;

        while (si >= 0 && ti >= 0) { 
            si = getNextValidIndex(s, si);
            ti = getNextValidIndex(t, ti);

            if (si == ti && si == -1) {
                return true;
            }

            if (si == -1 || ti == -1) {
                return false;
            }

            if (s.charAt(si) != t.charAt(ti)) {
                return false;
            }

            ti--;
            si--;
        }

        si = getNextValidIndex(s, si);
        ti = getNextValidIndex(t, ti);

        return si == ti;
    }

    private int getNextValidIndex(String str, int index) {
        int deleteCounter = 0;
        while (index >= 0) {
            char cur = str.charAt(index);
            if (cur == '#') {
                deleteCounter++;
                index--;
                continue;
            }

            if (deleteCounter == 0) {
                return index;
            } else {
                deleteCounter--;
                index--;
            }
        }

        return index;
    }
}
```
### Time
O(N) -- где N максимальная длина строки
### Memory
O(1) -- нам не нужна доп память, зависящая от длины строки
### Explication
Начинаем итерировать с конца строки, потому что `#` стираем предыдущие
символы. Итерируем с конца и ищем следующий валидный индекс.
1. Если индекс существует для обоих строк, проверяем символы по этим индексам 
   1. Если символы равны -- продолжаем поиск и отнимаем единицу у индексов.
   2. Если символы не равны -- возвращаем `false`.
2. Если индекс не существует (то есть строка стала пустой) для двух строк -- возвращаем `true`. Две строки стали пустыми
3. Если индекс не существует только для одной строки -- возвращаем `false`. Значит одна строка
стала пустой, а вторая еще имеет символы.
4. Если мы вышли из цикла, значит в одной из строк закончились символы для проверки. Чтобы убедиться
что строки точно равны или точно различны, мы еще один раз ищем следующий валидный индекс. Если два индекса
стали пустыми (равными -1) -- возвращаем `true`, иначе -- `false`.

Функция поиска валидного символа. В нее мы передаем текущую позицию. 
1. Если текущий индекс строго меньше 0 -- возвращаем этот же индекс.
2. Если символ по текущей позиции равен `#`, то переходим на след индекс и увеличиваем deleteCount на 1.
3. Если символ не равен `#`, то проверяем deleteCount
   1. если deleteCount == 0, значит мы нашли наш индекс.
   2. если deleteCount != 0, то отнимаем 1 у deleteCount и переходим на след индекс.