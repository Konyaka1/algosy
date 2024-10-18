## Fails
### 1st try
Messed up if condition
```java
class Solution {
    public String simplifyPath(String path) {
        Deque<String> deq = new ArrayDeque<>();
        for (String str : path.split("/")) { // HERE
            if (str.length() < 2) {
                continue;
            }
            if ("..".equals(str)) {
                deq.pollLast();
            } else {
                deq.offerLast(str);
            }
        }
        
        if (deq.isEmpty()) {
            return "/";
        }
        
        StringBuilder sb = new StringBuilder();
        while (!deq.isEmpty()) {
            sb.append("/");
            sb.append(deq.pollFirst());
        }
        return sb.toString();
    }
}
```