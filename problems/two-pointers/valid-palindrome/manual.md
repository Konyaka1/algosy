### Solution
```java
class Solution {
    public boolean isPalindrome(String s) {
        int l = 0;
        int r = s.length() - 1;

        while (l < r) {
            char leftSymbol = s.charAt(l);
            if (!Character.isLetterOrDigit(leftSymbol)) {
                l++;
                continue;
            }

            char rightSymbol = s.charAt(r);
            if (!Character.isLetterOrDigit(rightSymbol)) {
                r--;
                continue;
            }

            if (Character.toLowerCase(leftSymbol) != Character.toLowerCase(rightSymbol)) {
                return false;
            }
            l++;
            r--;
        }

        return true;
    }
}
```

### Time
O(N) -- потому что проходим по всему массиву
### Memory
O(1) -- независимо от длины строки мы храним только указатель на начало и конец.
### Explication
Идея проста -- ставим два указателя на начало и конец. В цикле находим валидный 
символ для начала и конца и сравниваем их.
