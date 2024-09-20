### Solution
TIME: дофига.
```java
class Solution {
    public void rotate(int[] nums, int k) {
        int steps = k % nums.length;
        if (steps == 0) {
            return;
        }

        rotate(nums, nums.length - steps, nums.length - 1);
        rotate(nums, 0, nums.length - 1 - steps);
        rotate(nums, 0, nums.length - 1);
    }

    private void rotate(int[] nums, int l, int r) {
        while (l < r) {
            int tmp = nums[l];
            nums[l] = nums[r];
            nums[r] = tmp;
            l++;
            r--;
        }
    }
}
```
### Time
O(N) -- Меняем позиции в массиве два раза
### Memory
O(1) -- не используем копию массива
### Explication
Говно говна. Свапаем местами последние k элементов между собой и первые n - k элементов между собой.
Затем меняем все элементы между собой. И магическим образом все становится в нужные места.
Объяснение снизу.
```
 0   1   2   3          n - 1
[x0, x1, x2, x3, ..., x[n - 1]]

so let's split array in two parts. first part is the amount of elements simply going to the right.
second part is elements going to left (to the start of the array).

   0   1        n - k - 2    n - k - 1        n - k      n - k + 1         n - 1
[ x0, x1 ..., x[n - k - 2], x[n - k - 1] ||| x[n - k], x[n - k + 1], ... x[n - 1] ]
         n - k elements                              k elements

swap elements inside sub ararys.

     0                 1        n - k - 2    n - k - 1         n - k            n - k + 1      n - 1
[ x[n - k - 1], x[n - k - 2], ..., x[1],         x[0] |||      x[n - 1], ..., x[n - k + 1],  x[n - k] ] 
     n - k elements                                                  k elements

swap all elements.
 
  0        1            k - 1      k             n - 2    n - 1  
[ x[k], x[k + 1], ..., x[n - 1],  x[0], ..., x[k - 2], x[k - 1]] 

explanation;

formula for new pos == last index - i-index + start index;
After first swap of sub arrays x[0] has position == n - k - 1, now we swap this position with mirrored one
pos of x[0] == n - k - 1;
do swap  --    (n - 1) - (n - k - 1) + 0 == n - 1 - n + k + 1 == k.
new pos of x[0] is k
new pos of x[1] is k + 1

pos of x[n - 1] == n - k
do swap --   (n - 1) - (n - k) == n - 1 - n + k == k - 1
new pos of x[n - 1] is k - 1;
new pos of x[n - 2] is k - 2;
```
