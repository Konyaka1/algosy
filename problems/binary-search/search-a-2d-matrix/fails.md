## Fails
### 1st try
Index out of bounds. Мы не можем присвоить ri значение больше индекса, потому что
оно сдвигает индекс в _"plain array"_ на rowLegnth позиций, а нам нужен
сдвиг на одну позицию.
```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        int lengthOfRow = matrix[0].length;

        int li = 0;
        int lj = 0;
        // HERE
        int ri = matrix.length;
        int rj = lengthOfRow;


        int lIndex = (li * lengthOfRow) + lj;
        int rIndex = (ri * lengthOfRow) + rj;
        while (rIndex - lIndex > 1) {
            int m = (rIndex + lIndex) / 2;

            int mi = m / lengthOfRow;
            int mj = m % lengthOfRow;
            if (matrix[mi][mj] <= target) {
                // move l
                li = mi;
                lj = mj;
                lIndex = m;
            } else {
                // move r
                ri = mi;
                rj = mj;
                rIndex = m;
            }
        }

        return target == matrix[li][lj];
    }
}
```