### Solution
Array based solution
```java
public class Solution {
    
    public ArrayList<Integer> intersect(final int[] A, final int[] B) {
        int i1 = 0;
        int i2 = 0;

        ArrayList<Integer> result = new ArrayList<>();

        while (i1 < A.length && i2 < B.length) {
            int an = A[i1];
            int bn = B[i2];

            if (an == bn) {
                result.add(an);
                i1++;
                i2++;
            } else if (an < bn) {
                i1++;
            } else {
                i2++;
            }

        }
        return result;
    }
}
```
Iterator based solution
```java
public class Solution {
    public ArrayList<Integer> intersect(final List<Integer> A, final List<Integer> B) {
        if (A.isEmpty() || B.isEmpty()) {
            return new ArrayList<>();
        }

        Iterator<Integer> first = A.iterator();
        Iterator<Integer> second = B.iterator();

        ArrayList<Integer> res = new ArrayList<>();


        int fn = first.next();
        int sn = second.next();

        while (first.hasNext() && second.hasNext()) {
            if (fn < sn) {
                fn = first.next();
            } else if (fn > sn) {
                sn = second.next();
            } else {
                res.add(fn);
                fn = first.next();
                sn = second.next();
            }
        }

        // one of the list is empty, let's move
        // them while they are less than other number

        // if first is not pointing to end, means second is pointing to end
        // so second number is the last
        // if first number is more than second we quit
        // if fn == sn we don't move
        while (first.hasNext() && fn < sn) {
            fn = first.next();
        }

        while (second.hasNext() && sn < fn) {
            sn = second.next();
        }

        if (fn == sn) {
            res.add(fn);
        }

        return res;
    }
}
```
### Time
O(N + M) -- потому что надо пройти по двум массивам
### Memory
O(K) -- память зависит от кол-ва пересеченных элементов, нужно для хранения ответа
### Explication
По скольку массивы отсортированы, мы можем двигать указатель для массива,
у которого текущий элемент меньше. Для массивов все очевидно.

Для листов, надо добавить пару проверок. Идея в том, что hasNext() возвращает false
на последнем элементе, и мы не проверяем последний элемент в цикле. 
Выйдя из основного цикла, мы знаем, что в результирующем массиве не хватает последнего элемента.
Для этого мы двигаемся по первому массиву пока можем. Аналогично делаем со вторым массивом.
Идем по листам пока там есть значения и пока значение меньше другого. Подвинув все листы 
делаем последнюю проверку на равенство и возвращаем ответ
