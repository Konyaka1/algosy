### Solution
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
                return false;
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

### Time
O(N) -- Потому что проходим каждый элемент
### Memory
O(N) -- Потому что храним в сет каждую точку, а их N
### Explication
Сначала нужно понять как вообще найти симметричную точку. Для этого надо знать потенациальную середину.
Для этого ищем две самые крайние точки, самую левую по иксу и самую правую по иксу.
Теперь чтобы для x1 найти симметричную x2 можно воспользоваться следующей идеей.
Расстояние от x1 до x-min == расстояние от x2 до x-max.

``(x1 - x-min) == (x-max - x2)``

``x2 == x-max - (x1 - x-min)``

Теперь найдя симетричную точку, надо проверить существует ли она в нашем set.

### Note
Лист в отличии от массива имеет полноценный equals. 