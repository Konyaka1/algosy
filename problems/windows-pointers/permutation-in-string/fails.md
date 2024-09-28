## Fails
### 1st try
Никогда больше не переписывать написанное. Сначала удалить, потом написать заново
```java
class Solution {
    public boolean checkInclusion(String s1, String s2) {
        if (s1.length() > s2.length()) {
            return false;
        }

        Map<Character, Integer> target = new HashMap<>();
        Map<Character, Integer> current = new HashMap<>();

        for (int i = 0; i < s1.length(); i++) {
            target.merge(s1.charAt(i), 1, Integer::sum);
            current.merge(s2.charAt(i), 1, Integer::sum);
        }
        
        if (target.equals(current)) {
                return true;
        }

        for (int i = s1.length(); i < s2.length(); i++) {
            current.merge(s2.charAt(i), 1, Integer::sum);
            
            char left = s2.charAt(i - s1.length());
            int leftFreq = current.get(left);
            if (leftFreq) == 1) {
                current.remove(left);
            } else {
                current.put(left, leftFreq - 1);
            }


            if (target.equals(current)) {
                return true;
            }
        }

        return false;
    }
}
```

ArrayBased, Index out of bounds.
```java
class Solution {
    public boolean checkInclusion(String s1, String s2) {
        if (s1.length() > s2.length()) {
            return false;
        }

        char[] target = new char[26];
        char[] current = new char[26];

        for (int i = 0; i < s1.length(); i++) {
            target[s1.charAt(i) - 'a']++;
            current[s2.charAt(i) - 'a']++;
        }

        if (Arrays.equals(target, current)) {
            return true;
        }

        for (int i = s1.length(); i < s2.length(); i++) {
            current[s2.charAt(i)]++; // HERE

            int left = i - s1.length();
            current[s2.charAt(left)]--; // HERE

            if (Arrays.equals(target, current)) {
                return true;
            }
        }

        return false;
    }
}
```