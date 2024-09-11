## Fails
### 1st try
[SYNTAX] STRING DOESN'T HAVE PROPERTY LENGTH. IT IS A **METHOD**. `p.length()`
```java

class Solution {
    public List<Integer> findAnagrams(String s, String p) {
        if (p.length() > s.length()) {
            return Collections.emptyList();
        }

        char[] requiredAnagram = new char[p.length()];
        char[] curAnagram = new char[p.length()];

        for (int i = 0; i < p.length; i++) {
            char pSymbol = p.charAt(i);
            requiredAnagram[pSymbol - 'a']++;

            char sSymbol = s.charAt(i);
            curAnagram[sSymbol - 'a']++;
        }

        List<Integer> result = new LinkedList<>();

        for (int i = 0; i <= s.length() - p.length(); i++) {
            if (equalsAnagrams(requiredAnagram, curAnagram)) {
                result.add(i);
            }

            int nextIndex = i + p.length();
            if (nextIndex < s.length()) {
                char next = s.charAt(nextIndex);
                curAnagram[next - 'a']++;

                char prev = s.charAt(i);
                curAnagram[prev - 'a']--;
            }
        }

        return result;
    }

    private boolean equalsAnagrams(char[] anagram1, char[] anagram2) {
        return Arrays.equals(anagram1, anagram2);
    }
}
```
### 2nd try
[LOGIC] anagram length is 26, not p.length().
```java
class Solution {
    public List<Integer> findAnagrams(String s, String p) {
        if (p.length() > s.length()) {
            return Collections.emptyList();
        }

        char[] requiredAnagram = new char[p.length()];
        char[] curAnagram = new char[p.length()];

        for (int i = 0; i < p.length(); i++) {
            char pSymbol = p.charAt(i);
            requiredAnagram[pSymbol - 'a']++;

            char sSymbol = s.charAt(i);
            curAnagram[sSymbol - 'a']++;
        }

        List<Integer> result = new LinkedList<>();

        for (int i = 0; i <= s.length() - p.length(); i++) {
            if (equalsAnagrams(requiredAnagram, curAnagram)) {
                result.add(i);
            }

            int nextIndex = i + p.length();
            if (nextIndex < s.length()) {
                char next = s.charAt(nextIndex);
                curAnagram[next - 'a']++;

                char prev = s.charAt(i);
                curAnagram[prev - 'a']--;
            }
        }

        return result;
    }

    private boolean equalsAnagrams(char[] anagram1, char[] anagram2) {
        return Arrays.equals(anagram1, anagram2);
    }
}
```