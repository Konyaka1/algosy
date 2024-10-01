## Fails
### 1st try
да как так, забыл точку с запятой
```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int l = 0 // HERE
        int r = -1;
        
        int maxLength = 0;
        Set<Character> set = new HashSet<>();
        
        while (l < s.length()) {
            while (r + 1 < s.length() && set.add(s.charAt(r + 1))) {
                r = r + 1;
            }
            
            maxLength = Math.max(maxLength, set.size());
            
            set.remove(s.charAt(l));
            l = l + 1;
        }
        
        return maxLength;
    }
}

```