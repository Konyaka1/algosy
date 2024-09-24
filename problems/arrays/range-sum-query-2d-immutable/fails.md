## Fails
### 1st try
Error in syntax with 3d array.
```java
class NumMatrix {

    final int[][] prMatr;

    public NumMatrix(int[][] matrix) {
        int m = matrix.length;
        int n = matrix[0].length;

        this.prMatr = new int[m + 1][n + 1];

        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                this.prMatr[i + 1][j + 1] = matrix[i][j] + this.prMatr[i][j + 1] + this.prMatr[i + 1][j] - this.prMatr[i][j];
            }
        }
    }

    public int sumRegion(int row1, int col1, int row2, int col2) {
        int wholeRegion = this.prMatr[row2 + 1][col2 + 1];
        int leftRegion = this.prMatr[row2 + 1][col1];
        int upRegion = this.prMatr[row1][col2 + 1];
        int intersectionRegion = this.prMatr[row1, col1]; // HERE

        return wholeRegion - leftRegion - upRegion + intersectionRegion;
    }
}
```