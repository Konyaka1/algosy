## Fails
Not correctly created xor prefix arr
```java
class Solution {
    public int[] xorQueries(int[] arr, int[][] queries) {
        int[] prArr = new int[arr.length + 1];
        prArr[0] = arr[0];
        for (int i = 0; i < arr.length; i++) {
            prArr[i + 1] = prArr[i] ^ arr[i];
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