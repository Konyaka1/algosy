### Solution 1
Bin search solution
```java
class Solution {
    public List<Integer> findClosestElements(int[] arr, int k, int x) {
        int l = 0;
        int r = arr.length - k + 1;

        while (r - l > 1) {
            int m = (r + l) / 2;

            if (this.isGood(arr[m - 1], arr[m + k - 1], x)) {
                l = m;
            } else {
                r = m;
            }
        }

        List<Integer> res = new ArrayList<>(k);
        for (int i = l; i < l + k; i++) {
            res.add(arr[i]);
        }

        return res;
    }

    private boolean isGood(int nextStart, int currEnd, int target) {
        // another version
        // return target - nextStart > currEnd - target; 
        return nextStart - target < target - currEnd;
    }
}
```
### Time
O(log N) -- делаем бинарный поиск
### Memory
O(K) -- Память для ответа.
### Explication
Для бинарного поиска мы ищем начало ответа. Нам надо найти все возможные начало ответа.
Для этого мы находим середину и считаем ее как потенциальное начало. Теперь надо убедиться,
что это начало лучше предыдущего начала. Для этого сравниваем предыдущий от середины `m - 1` и конец
текущего `m + k - 1`. Если левое ближе --> возвращаем `false`, чтобы подвинуть правый указатель.
### Solution 2
Regular linear solution
```java
class Solution {
    public List<Integer> findClosestElements(int[] arr, int k, int x) {
        int l = 0;
        int r = arr.length - 1;

        while (r - l + 1 > k) {
            if (this.isFirstCloser(arr[l], arr[r], x)) {
                r--;
            } else {
                l++;
            }
        }

        List<Integer> result = new ArrayList<>(k);
        for (int i = l; i < r + 1; i++) {
            result.add(arr[i]);
        }

        return result;
    }

    private boolean isFirstCloser(int a, int b, int x) {
        return Math.abs(a - x) <= Math.abs(b - x);
    }
}
```
### Time
O(N - K) -- делаем n - k сравнений, пока размер окна не будет равен размеру необходимому
### Memory
O(K) -- k размер ответа, а вообще память доп не нужна
### Explication
Ставим два указателя, и двигаем тот, который дальше от ответа.
