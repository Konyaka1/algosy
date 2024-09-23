## Fails
### 1st try
Не поставил отрицание на проверке isLetterOrDigit.
```java
class Solution {
    public boolean isPalindrome(String s) {
        int left = 0;
        int right = s.length() - 1;

        while (left < right) {
            char leftSymbol = s.charAt(left);
            while (Character.isLetterOrDigit(leftSymbol)) { // HERE
                left++;
                if (left == s.length()) {
                    return true;
                }

                leftSymbol = s.charAt(left);
            }

            char rightSymbol = s.charAt(right);
            while (Character.isLetterOrDigit(rightSymbol)) { // HERE
                right--;
                if (right == -1) {
                    return true;
                }

                rightSymbol = s.charAt(right);
            }

            if (leftSymbol != rightSymbol) {
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
### 2nd try
Забыл поставить привести символы к нижнему регистру.
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
            
            if (leftSymbol != rightSymbol) { // HERE
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