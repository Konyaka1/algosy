### Solution
Bin search solution
```java
class Solution {
    public void twoSum() {

    }
}
```
Regular linear solution
```java
class Solution {
    public List<Integer> findClosestElements(int[] arr, int k, int x) {
        int l = 0;
        int r = arr.length - 1;

        while (r - l + 1 > k) {
            if (this.isFirstCloser(arr[l], arr[r], x)) {
                r--;
            } else {
                l++;
            }
        }

        List<Integer> result = new ArrayList<>(k);
        for (int i = l; i < r + 1; i++) {
            result.add(arr[i]);
        }

        return result;
    }

    private boolean isFirstCloser(int a, int b, int x) {
        return Math.abs(a - x) <= Math.abs(b - x);
    }
}
```
### Time
O(1) -- потому что 
### Memory
O(1) -- потому что
### Explication
Потому что