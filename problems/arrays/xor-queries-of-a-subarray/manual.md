### Solution
TIME: ~40min.
```java
class Solution {
    public int[] xorQueries(int[] arr, int[][] queries) {
        int[] prArr = new int[arr.length];
        prArr[0] = arr[0];
        for (int i = 1; i < arr.length; i++) {
            prArr[i] = prArr[i - 1] ^ arr[i];
        }

        int[] result = new int[queries.length];
        for (int i = 0; i < queries.length; i++) {
            int l = queries[i][0];
            int r = queries[i][1];
            // xor[l, r] == xor[0, r] ^ xor[0, l - 1]
            result[i] = prArr[r];
            if (l != 0) {
                result[i] = result[i] ^ prArr[l - 1];
            }
        }

        return result;
    }
}
```
### Time
O(N + q) -- N потому что создаем префиксный массив для N элементов, q -- количество кверей для подсчета
### Memory
O(N) -- храним префиксный массивы
### Explication
Для понятия идеи решения нужно знать главное свойство xor: `a ^ a == 0` или более наглядно 
`a ^ b ^ c ^ d ^ b ^ c = a ^ d`. Для создания префиксного массива надо понимать, что в качестве нулевого элемента нельзя
использовать 0. Потому что для xor 0 не является нейтральным элементом.
Краткое описание xor prefix array:
```
arr[0] = x0
arr[1] = x0 ^ x1 == arr[0] ^ x1
arr[2] = x0 ^ x1 ^ x2 == arr[1] ^ x2
arr[3] = x0 ^ x1 ^ x2 ^ x3 == arr[2] ^ x3
...
arr[i] = arr[i - 1] ^ xi
```
Далее для подсчета каждой квери, надо понять, что левый указатель равный нулю `q[i][0]`
означает полноценный xor от 0 до r. То есть `query[i] == [0, 3]` означает
`x0 ^ x1 ^ x2 ^ x3`. Для любого другого случая, нам надо повторяющиеся элементы.

Считаем что квери от 3 до 5. Значит нам надо вернуть `x3 ^ x4 ^ x5`. В массиве мы имеем:
```
arr[2] = x0 ^ x1 ^ x2
arr[5] = x0 ^ x1 ^ x2 ^ x3 ^ x4 ^ x5
```
Значит чтобы найти будет верно тождество
```
x3 ^ x4 ^ x5 == (x0 ^ x1 ^ x2 ^ x3 ^ x4 ^ x5) ^ (x0 ^ x1 ^ x2) == arr[5] ^ arr[2];
```
Или в общем виде
```
xor(l, r) == arr[r] ^ arr[l - 1], где 0 < l <= r.
xor(0, r) == arr[r], r >= 0
```