### Solution
```java
public class Solution {
    
    public boolean isOneEditDistance(String s, String t) {
        if (s.length() > t.length()) {
            return isOneEditDistance(t, s);
        }

        if (t.length() - s.length() > 1) {
            return false;
        }

        boolean isEqual = t.length() == s.length();

        int prtS = 0;
        int prtT = 0;

        while (prtS < s.length()) {
            if ( s.charAt(prtS) != t.charAt(prtT) ) {
                if (isEqual) {
                    return isEqualSubString(s, t, prtS + 1, prtT + 1);
                } else {
                    return isEqualSubString(s, t, prtS + 1, prtT + 2);
                }
            }
            prtS++;
            prtT++;
        }

        return !isEqual;
    }

    private boolean isEqualSubString(String s, String t, int startS, int startT) {
        while (startS < s.length()) {
            if ( s.charAt(startS) != t.charAt(startT) ) {
                return false;
            }
            startS++;
            startT++;
        }
        return true;
    }
}
```
One more solution
```java
public class Solution {
    
    public boolean isOneEditDistance(String s, String t) {
        if (s.length() > t.length()) {
            return this.isOneEditDistance(t, s);
        }

        if (t.length() - s.length() > 1) {
            return false;
        }
        
        int si = 0;
        int ti = 0;

        while (si < s.length() && s.charAt(si) == t.charAt(ti)) {
            si++;
            ti++;
        }

        if (t.length() == s.length()) {
            if (si == s.length()) {
                return false;
            }
            return this.isSameStrings(s, t, si + 1, ti + 1);
        } else {
            if (si == s.length()) {
                return true;
            }
            return this.isSameStrings(s, t, si, ti + 1);
        }
    }

    private boolean isSameStrings(String s, String t, int si, int ti) {
        while (si < s.length()) {
            if (s.charAt(si) != t.charAt(ti)) {
                return false;
            }
            si++;
            ti++;
        }

        return true;
    }
}
```
### Time
O(N) -- потому что проходим по всей строке
### Memory
Изначально мы можем сразу вернуть false, если разница в длине строк больше 1.
Далее мы делаем рекурсивный вызов, чтобы длина первой строки всегда была меньше или
равна длине второй строки. Дальше логика проста: Идем по строчкам и ищем первый не одинаковый символ.
Как только разница найдена -- проверяем концы двух строк на равенство. Если строки равны по длине
то мы не проверяем концы строк со след индексов, если нет -- то смещаем конец второй строки на единицу.

Если мы прошли весь цикл, а разницу не нашли, то есть два случая: строки равны между собой ИЛИ 
эти строки отличаются на последний элемент ("a", "ac"). Соответственно возвращаем `!isEqual`.

Визуализация: Равная длина
```
    s0, ... s[k-1],     X,    s[k+1], ... s[n-1]
    t0, ... t[k-1],     Y,    t[k+1], ... t[n-1]
equal from 0 to k - 1  DIFF    rest of string
```
Визуализация: Разная длина
```
    s0, ... s[k-1],    s[k], ... s[n-1]
    t0, ... t[k-1],     Y,  t[k+1], ... t[n],
equal from 0 to k - 1  DIFF    rest of string
```