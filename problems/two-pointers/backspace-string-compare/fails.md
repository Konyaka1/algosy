## Fails
### 1st try
Didn't handle the case, when one string is empty, and second is not.
```java
class Solution {
    public boolean backspaceCompare(String s, String t) {
        int si = s.length() - 1;
        int ti = t.length() - 1;

        while (si >= 0 && ti >= 0) { // si = 0, ti == 2
            si = getNextValidIndex(s, si);
            ti = getNextValidIndex(t, ti);

            if (si == ti && si == -1) {
                return true;
            }
            // HERE

            if (s.charAt(si) != t.charAt(ti)) {
                return false;
            }

            ti--;
            si--;
        }

        si = getNextValidIndex(s, si);
        ti = getNextValidIndex(t, ti);

        return si == ti;
    }

    private int getNextValidIndex(String str, int index) {
        int deleteCounter = 0;
        while (index >= 0) {
            char cur = str.charAt(index);
            if (cur == '#') {
                deleteCounter++;
                index--;
                continue;
            }

            if (deleteCounter == 0) {
                return index;
            } else {
                deleteCounter--;
                index--;
            }
        }
        
        return index;
    }
}
```