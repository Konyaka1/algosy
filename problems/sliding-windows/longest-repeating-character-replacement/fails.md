## Fails
### 1st try
FORGOT TO MOVE LEFT POINTER TABARNAK
```java
class Solution {
    public int characterReplacement(String s, int k) {
        if (k < 1) {
            return 0;
        }
        
        int l = 0;
        int r = -1;
        
        int maxLength = 0;
        int[] map = new int[26];
        int[] curMax = {0};
        while (r + 1 < s.length()) {
            while (this.canOffer(s, l, r + 1, k, map, curMax)) {
                r = r + 1;
            }
            
            maxLength = Math.max(r - l + 1, maxLength);
            
            // move left
            map[s.charAt(l) - 'A']--;
            for (int fr : map) {
                if (fr > curMax[0]) {
                    curMax[0] = fr;
                }
            }
            // HERE
        }
        
        return maxLength;
    }
    
    private boolean canOffer(String s, int l, int r, int k, int[] map, int[] max) {
        if (r >= s.length()) {
            return false;
        }
        char curCh = s.charAt(r);
        map[curCh - 'A']++;
        int prevMax = max[0];
        max[0] = Math.max(max[0], map[curCh - 'A']);
        
        int curK = (r - l + 1) - max[0];
        if (curK > k) {
            max[0] = prevMax;
            map[curCh - 'A']--;
            return false;
        } else {
            return true;
        }
    }
}
```
### 2nd try
Stupid check for k.
```java
class Solution {
    public int characterReplacement(String s, int k) {
        // HERE
        if (k < 1) {
            return 0;
        }
        
        int l = 0;
        int r = -1;
        
        int maxLength = 0;
        int[] map = new int[26];
        int[] curMax = {0};
        while (r + 1 < s.length()) {
            while (this.canOffer(s, l, r + 1, k, map, curMax)) {
                r = r + 1;
            }
            
            maxLength = Math.max(r - l + 1, maxLength);
            
            // move left
            map[s.charAt(l) - 'A']--;
            for (int fr : map) {
                if (fr > curMax[0]) {
                    curMax[0] = fr;
                }
            }
            l = l + 1;
        }
        
        return maxLength;
    }
    
    private boolean canOffer(String s, int l, int r, int k, int[] map, int[] max) {
        if (r >= s.length()) {
            return false;
        }
        char curCh = s.charAt(r);
        map[curCh - 'A']++;
        int prevMax = max[0];
        max[0] = Math.max(max[0], map[curCh - 'A']);
        
        int curK = (r - l + 1) - max[0];
        if (curK > k) {
            max[0] = prevMax;
            map[curCh - 'A']--;
            return false;
        } else {
            return true;
        }
    }
}
```