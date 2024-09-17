### Solution
TIME: 18:55.
```java
class NumArray {

    private final int[] prArr;

    public NumArray(int[] nums) {
        this.prArr = new int[nums.length + 1];
        for (int i = 1; i < nums.length + 1; i++) {
            this.prArr[i] = this.prArr[i - 1] + nums[i - 1];
        }
    }

    public int sumRange(int left, int right) {
        return this.prArr[right + 1] - this.prArr[left];
    }
}
```
### Time
- creation: O(N) -- проходим через весь массив изначальный.
- sum range: O(1) -- обычная разность двух чисел
### Memory
- creation: O(N) -- создается массив длины n + 1.
- sum range: O(1) -- не нужна доп память для подсчета
### Explication
Храним массив сумм. То есть x[i + 1] = x0 + x1 + ... + xi, потому что храним x[0] == 0.
для получения суммы 2, 5 мы берем x[6] - x[2], потому что:
`x[6] - x[2] == (x0 + x1 + x2 + x3 + x4 + x5) - (x0 + x1) == x2 + x3 + x4 + x5`
