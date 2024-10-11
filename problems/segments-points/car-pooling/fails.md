## Fails
### 1st try
Forgot to sort points using array
```java
class Solution {
    public boolean carPooling(int[][] trips, int capacity) {
        Comparator<int[]> comp = (a, b) -> {
            if (a[0] == b[0]) {
                return Integer.compare(a[1], b[1]);
            } else {
                return Integer.compare(a[0], b[0]);
            }
        };
        
        int[][] points = new int[trips.length * 2][2];
        
        int i = 0;
        for (int[] trip : trips) {
            points[i++] = new int[] {trip[1], trip[0]};
            points[i++] = new int[] {trip[2], -trip[0]};
        }
        // HERE
        
        int curPass = 0;
        for (int[] point : points) {
            curPass += point[1];
            if (curPass > capacity) {
                return false;
            }
        }
        
        return true;
    }
} 
```