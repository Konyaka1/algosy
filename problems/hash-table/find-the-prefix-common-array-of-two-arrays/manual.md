### Solution
```java
class Solution {
    public int[] findThePrefixCommonArray(int[] A, int[] B) {
        Set<Integer> setA = new HashSet<>();
        Set<Integer> setB = new HashSet<>();
        
        int[] result = new int[A.length];
        
        result[0] = A[0] == B[0] ? 1 : 0;
        setA.add(A[0]);
        setB.add(B[0]);
        
        // setA [1]  setB [3]
        for (int i = 1; i < result.length - 1; i++) {
            // i = 1
            int ai = A[i]; // 3
            int bi = B[i]; // 1
            
            result[i] = result[i - 1] + (setA.contains(bi) ? 1 : 0) + (setB.contains(ai) ? 1 : 0) + (ai == bi ? 1 : 0);
            // 2 = 0 + 1 + 1 + 0
            setA.add(ai);
            setB.add(bi);
        }
        
        result[result.length - 1] = result.length;
        
        return result;
    }
}
```
Решение без set.
```java
class Solution {
    public int[] findThePrefixCommonArray(int[] A, int[] B) {
        // step 0.
        int[] visited = new int[A.length];
        // step 1.
        int[] result = new int[A.length];
        // step 2.

        result[0] = A[0] == B[0] ? 1 : 0; 
        visited[A[0] - 1]++; 
        visited[B[0] - 1]++; 
        // step 3.
        for (int i = 1; i < A.length - 1; i++) {
            // step 3.1.
            if (A[i] == B[i]) {
                result[i] = result[i - 1] + 1;
            } else {

                visited[A[i] - 1]++;
                visited[B[i] - 1]++;
                result[i] = result[i - 1] + (visited[A[i] - 1] == 2 ? 1 : 0) + (visited[B[i] - 1] == 2 ? 1 : 0);
            }
        }
        // step 4.
        result[A.length - 1] = A.length;
        
        return result;
    }
}
```
Решение на битовых операциях
```java
class Solution {
    
    public int[] findThePrefixCommonArray(int[] A, int[] B) {
        long visitedFirst = 0;
        long visitedSecond = 0;
        
        int[] result = new int[A.length];
        for (int i = 0; i < A.length; i++) {
            visitedFirst = visitedFirst | (1L << A[i]);
            visitedSecond = visitedSecond | (1L << B[i]);

            result[i] = Long.bitCount(visitedFirst & visitedSecond);
        }
        
        return result;
    }
}
```
### Time
O(N) -- Потому что проходим каждый элемент
### Memory
O(N) -- Потому что храним каждый элемент в set + размер ответа
### Explication
поскольку все числа от 1 до n встречаются по одному разу гарантировано в каждом массиве
означает что в последний элемент ответа будет равен длине массива.

Также первый элемент будет равен либо 0 либо 1 в зависимости от равенства первых элементов

Заводим set для каждого массива, в котором хранятся уже пройденные элементы.
Далее итерируем все кроме первого и последнего. После каждого прохода добавляем только что пройденные элементы в set 

```c[i] = c[i - 1] + setA.contains(b[i]) + setB.contains(a[i]) + a[i] == b[i]```

Важно не забыть добавить ```a[i] == b[i]```, потому что два равных элемента, означают, что в 
set-ах они не будут храниться.

Кратко в задаче есть два действия -- добавить элементы в сет и узнать текущее пересечение этих сетов.

Для решения с использованием массива мы храним счетчик текущих пересечений. Каждую итерацию он либо увеличиться, 
либо останется на месте. Пересечение достигается при добавлении одинаковых элементов, или когда элемент массива 
равен 2 -- то есть мы уже встретили одинаковые элементы из двух множеств.

Для решения на битовых операциях, мы устанавливаем биты в двух "сетах" (лонгах) в 1.
Пересечение достигается обычной операцией &. Далее с помощью `Long.bitCount` достаем кол-во
пересеченных элементов.

### Note
Джава не приводит boolean к int автоматически