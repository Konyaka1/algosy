## Fails
### 1st try
Messed up comparison
```java
class Solution {
    public int[][] intervalIntersection(int[][] firstList, int[][] secondList) {
        List<int[]> res = new ArrayList<>();

        int fp = 0;
        int sp = 0;

        while (fp < firstList.length && sp < secondList.length) {
            int[] fdot = firstList[fp];
            int[] sdot = secondList[sp];

            int max = Math.max(fdot[0], sdot[0]);
            int min = Math.min(fdot[1], sdot[1]);
            if (max <= min) {
                int[] dot = new int[]{max, min};
                res.add(dot);
                if (min == sdot[1]) { // HERE
                    fp++;
                } else {
                    sp++;
                }
            } else {
                if (fdot[0] > sdot[1]) {
                    sp++;
                } else {
                    fp++;
                }
            }
        }

        return res.toArray(new int[0][]);
    }
}
```
### 2nd try
Messed up comparison again
```java
class Solution {
    public int[][] intervalIntersection(int[][] firstList, int[][] secondList) {
        List<int[]> res = new ArrayList<>();

        int fp = 0;
        int sp = 0;

        while (fp < firstList.length && sp < secondList.length) {
            int[] fdot = firstList[fp];
            int[] sdot = secondList[sp];

            int max = Math.max(fdot[0], sdot[0]); 
            int min = Math.min(fdot[1], sdot[1]);  
            if (max <= min) {
                int[] dot = new int[]{max, min};
                res.add(dot);
                if (min == sdot[0]) { // HERE
                    fp++;
                } else {
                    sp++;
                }
            } else {
                if (fdot[0] > sdot[1]) {
                    sp++;
                } else {
                    fp++;
                }
            }
        }

        return res.toArray(new int[0][]);
    }
}
```