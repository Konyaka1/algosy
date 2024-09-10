## Fails
#### 1st error
[LOGIC] Вместо return false в случае отсутсвия симметрии написал return true. Задача всегда возвращала true
```java
class Solution {


    public boolean isReflected(int[][] dots) {
        if (dots.length == 0) {
            return true;
        }

        int minX = dots[0][0];
        int maxX = dots[0][0];

        Set<List<Integer>> setOfDots = new HashSet<>();

        for (int[] dot : dots) {
            if (minX > dot[0]) {
                minX = dot[0];
            }
            if (maxX < dot[0]) {
                maxX = dot[0];
            }
            setOfDots.add(Arrays.asList(dot[0], dot[1]));
        }

        for (int[] dot : dots) {
            List<Integer> symDot = getSymmetric(dot, minX, maxX);

            if (!setOfDots.contains(symDot)) {
                return true;
            }
        }

        return true;
    }

    private List<Integer> getSymmetric(int[] dot, int minX, int maxX) {
        int symX = maxX + minX - dot[0];
        return Arrays.asList(symX, dot[1]);
    }
}
```
