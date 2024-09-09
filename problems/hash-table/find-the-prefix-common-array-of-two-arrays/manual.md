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
### Note
Джава не приводит boolean к int автоматически

Много ошибок очень, занервничал из-за нехватки времени, хотя додумался до формулы, и комментами правильно решение написал.