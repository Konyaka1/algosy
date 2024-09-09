## Fails
#### 1st error
String `length()` is **method**. It's not **property**.
```java
class Solution {
    public boolean isIsomorphic(String s, String t) {
        Map<Character, Character> mapS = new HashMap<>();
        Map<Character, Character> mapT = new HashMap<>();
        // foo and bar
        for (int i = 0; i < s.length; i++) { // string length is method, not a property.
            Character si = s.charAt(i); // o
            Character ti = t.charAt(i); // r

            if (isOverwritten(mapS, si, ti) || isOverwritten(mapT, ti, si)) {
                return false;
            }
        }

        return true;
    }
    // mapS: [f -> b, o -> a]
    // mapT: [b -> f, a -> o]
    private boolean isOverwritten(Map<Character, Character> map, Character key, Character value) { // k: o, v: r
        Character prevVal = map.put(key, value); // a
        if (prevVal == null) {
            return false;
        }

        return !value.equals(prevVal);
    }
}
```