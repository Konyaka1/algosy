## Fails
### 1st try
Wrong 'if else' in second cycle
```java
class Solution {
    public String minRemoveToMakeValid(String s) {
        int state = 0;
        int vl = 0;
        for (char ch : s.toCharArray()) {
            if (ch == '(') {
                state++;
            } else if (ch == ')' && state != 0) {
                vl++;
                state--;
            }
        }

        int vr = vl;
        StringBuilder sb = new StringBuilder();
        for (char ch : s.toCharArray()) {
            if (ch == '(' && vl > 0) {
                sb.append(ch);
                vl--;
            } else if (ch == ')' && vl < vr) {
                sb.append(ch);
                vr--;
            } else {
                sb.append(ch);
            }
        }
        return sb.toString();
    }
}
```