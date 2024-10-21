### Solution
```java
class Solution {

    private final Random rand = new Random();

    public int[] sortArray(int[] nums) {
        this.sort(nums, 0, nums.length);

        return nums;
    }

    private void sort(int[] nums, int l, int r) {
        if (r - l < 2) {
            return;
        }

        int pi = hoarePartition(nums, l, r);

        sort(nums, l, pi);
        sort(nums, pi + 1, r);
    }

    private int hoarePartition(int[] nums, int l, int r) {
        int randIndex = randIndex(l ,r);
        int pivot = nums[randIndex];

        swap(l, randIndex, nums);
        int i = l + 1;
        int j = r - 1;

        while (i <= j) {
            if (nums[i] < pivot) {
                i++;
            } else if (nums[j] > pivot) {
                j--;
            } else {
                swap(i, j, nums);
                i++;
                j--;
            }
        }

        swap(l, j, nums);

        return j;
    }

    private int randIndex(int l, int r) {
        return this.rand.nextInt(r - l) + l;
    }

    private void swap(int l, int r, int[] nums) {
        int tmp = nums[l];
        nums[l] = nums[r];
        nums[r] = tmp;
    }
}
```
### Time
O(N logN) -- потому что 
### Memory
O(log N) -- рекурсивный алгоритм
### Explication
Алгоритм быстрой сортировки заключается в делении массива на две части.
В левой части все элементы меньшие или равные опорному элементу, а в правой -- большие либо равные.
Соответственно как поделить массив на две части?

Сначала выбираем опорный элемент. Способов выбора очень много, разберем рандомный выбор.
Рандомно выбираем index элемента и это и есть наш опорный элемент. Ставим его на первую позицию. Далее
проходим по массиву двумя указателями, левым и правым. Далее увеличиваем левый, если элемент строго меншье
опорного. Увеличиваем правый, если правый строго больше опорного. Если эти условия не выполняются, то свапаем местами
элементы в позиции левого и правого элементов. Как вышли из цикла, надо вернуть опорный элемент на место.
Для этого делаем свап по первому индексу и правому.

Повторяем алгоритм рекурсивно для получившейся левой и правой части.
