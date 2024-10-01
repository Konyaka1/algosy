### Solution
Left based first. Сначала ищем _последнее_ вхождение
```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
        if (nums.length == 0) {
            return new int[]{-1, -1};
        }

        int l = 0;
        int r = nums.length;

        while (r - l > 1) {
            int m = (r + l) / 2;
            if (this.isLessOrEqual(nums[m], target)) {
                l = m;
            } else {
                r = m;
            }
        }

        if (nums[l] != target) {
            return new int[]{-1, -1};
        }

        int rightAnswer = l;
        r = l;
        l = -1;

        while (r - l > 1) {
            int m = (r + l) / 2;
            if (this.isLess(nums[m], target)) {
                l = m;
            } else {
                r = m;
            }
        }

        return new int[]{r, rightAnswer};


    }

    private boolean isLessOrEqual(int xi, int target) {
        return xi <= target;
    }

    private boolean isLess(int xi, int target) {
        return xi < target;
    }
}
```
Right based first. Сначала ищем _первое_ вхождение
```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
        if (nums.length == 0) {
            return new int[]{-1,-1};
        }

        int l = -1;
        int r = nums.length - 1;

        while (r - l > 1) {
            int m = (l + r) / 2;
            if (this.isStrictLess(nums[m], target)) {
                l = m;
            } else {
                r = m;
            }
        }
        if (nums[r] != target) {
            return new int[]{-1,-1};
        }
        int leftAnswer = r;

        l = r;
        r = nums.length;

        while (r - l > 1) {
            int m = (l + r) / 2;
            if (this.isLessOrEqual(nums[m], target)) {
                l = m;
            } else {
                r = m;
            }
        }

        return new int[]{leftAnswer, l};
    }

    private boolean isStrictLess(int xi, int target) {
        return xi < target;
    }

    private boolean isLessOrEqual(int xi, int target) {
        return xi <= target;
    }
}
```
### Time
O(log N) -- binary search
### Memory
O(1) -- нет нужды в доп памяти зависящей от длины массива
### Explication
Делаем бинарный поиск. Сначала ищем первое вхождение, если его нет -- возвращаем `{-1,-1}`.
Иначе ищем последнее вхождение. Для этого можно подвинуть индекс на позицию r. На асимптотику не влияет.
