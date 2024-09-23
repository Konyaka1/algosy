### Solution
```java
class Solution {
    public boolean isPalindrome(String s) {
        int left = 0;
        int right = s.length() - 1;

        while (left < right) {
            char leftSymbol = s.charAt(left);
            while (!Character.isLetterOrDigit(leftSymbol)) {
                left++;
                if (left == s.length()) {
                    return true;
                }

                leftSymbol = s.charAt(left);
            }

            char rightSymbol = s.charAt(right);
            while (!Character.isLetterOrDigit(rightSymbol)) {
                right--;
                if (right == -1) {
                    return true;
                }

                rightSymbol = s.charAt(right);
            }

            if (Character.toLowerCase(leftSymbol) != Character.toLowerCase(rightSymbol)) {
                return false;
            } else {
                left++;
                right--;
            }
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

Решение написано не очень красиво -- в retry чтобы написать лучше.
