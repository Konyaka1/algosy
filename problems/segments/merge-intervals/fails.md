## Fails
### 1st try
Messed up comparator
```java
class Solution {
    public int[][] merge(int[][] intervals) {
        Comparator<int[]> comp = (a, b) -> b[0] - a[0];

        Arrays.sort(intervals, comp);

        List<int[]> res = new ArrayList<>(intervals.length);
        res.add(intervals[0]);

        for (int i = 1; i < intervals.length; i++) {
            int[] last = res.get(res.size() - 1);
            if (this.isIntersected(last, intervals[i])) {
                this.merge(last, intervals[i]);
            } else {
                res.add(intervals[i]);
            }
        }

        return res.toArray(new int[0][]);
    }

    private boolean isIntersected(int[] a, int[] b) {
        return Math.max(a[0], b[0]) <= Math.min(a[1], b[1]);
    }

    private void merge(int[] a, int[] b) {
        a[0] = Math.min(a[0], b[0]);
        a[1] = Math.max(a[1], b[1]);
    }
}
```