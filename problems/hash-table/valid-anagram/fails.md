## Fails
### 1st try
[LOGIC] Forgot to check constraints. Assumed that length are always the same
```java
class Solution {
    public boolean isAnagram(String s, String t) {
        int[] freqs = new int[26];

        for (int i = 0; i < s.length(); i++) {
            int sChar = s.charAt(i);
            int tChar = t.charAt(i);

            freqs[sChar - 'a']++;
            freqs[tChar - 'a']--;
        }

        for (int curFreq : freqs) {
            if (curFreq != 0) {
                return false;
            }
        }

        return true;
    }
}
```