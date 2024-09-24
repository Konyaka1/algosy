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

        ArrayList<Integer> result = new ArrayList<>();

        Iterator<Integer> first = A.iterator();
        Iterator<Integer> second = B.iterator();

        int firstNumber = first.next();
        int secondNumber = second.next();
        while (first.hasNext() && second.hasNext()) {
            if (firstNumber > secondNumber) {
                secondNumber = second.next();
            } else if (firstNumber < secondNumber) {
                firstNumber = first.next();
            } else {
                result.add(firstNumber);
                firstNumber = first.next();
                secondNumber = second.next();
            }
        }
    
        while (first.hasNext() && firstNumber <= secondNumber) {
            if (firstNumber == secondNumber) {
                result.add(firstNumber);
                return result;
            }
            firstNumber = first.next();
        }
    
        while (second.hasNext() && secondNumber <= firstNumber) {
            if (firstNumber == secondNumber) {
                result.add(firstNumber);
                return result;
            }
            secondNumber = second.next();
        }
        
        if (firstNumber == secondNumber) {
            result.add(firstNumber);
        }
        

        return result;
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
Если в процессе движения по листам нашли последнее совпадение --> добавляем его в ответ и возвращаем результат.
Если мы не нашли совпадений в процессе движения до последних элементов, то просто сравниваем последние элементы
и возвращаем результат
