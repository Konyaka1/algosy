### Solution
```go
func isIsomorphic(s string, t string) bool {
	mapT := make(map[byte]byte)
	mapS := make(map[byte]byte)

	for i := range len(s) {
		if val, ok := mapT[s[i]]; ok && val != t[i] {
			return false
		} else {
			mapT[s[i]] = t[i]
		}

		if val, ok := mapS[t[i]]; ok && val != s[i] {
			return false
		} else {
			mapS[t[i]] = s[i]
		}
	}

	return true
}
```
Первое решение универсальное для любых символов.
```java
class Solution {
    public boolean isIsomorphic(String s, String t) {
        Map<Character, Character> mapS = new HashMap<>();
        Map<Character, Character> mapT = new HashMap<>();
        // foo and bar
        for (int i = 0; i < s.length(); i++) {
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
Второе решение для ascii символов, которое оптимальней для этой задачи
```java
class Solution {
    public boolean isIsomorphic(String s, String t) {
        int[] mapS = new int[256];
        int[] mapT = new int[256];
        // foo and bar
        for (int i = 0; i < s.length(); i++) {
            char si = s.charAt(i); // o
            char ti = t.charAt(i); // r
            
            if (isOverwritten(mapS, si, ti) || isOverwritten(mapT, ti, si)) {
                return false;
            }
        }
        
        return true;
    }
    
    private boolean isOverwritten(int[] map, char key, char value) { 
        int prev = map[key];
        map[key] = value;
        
        if (prev == 0) {
            return false;
        }
        
        return value != prev;
    }
}
```

### Time
O(N) -- Потому что проходим через всю строку
### Memory
**Первое решение**

O(K) -- где K, это количество уникальных символов. Потому что храним маппинг каждого элемента

**Второе решение**

O(1) -- Потому что количество символов константно

### Explication
Храним маппинг каждой строки и сравниваем с уже имеющимся маппингом. Решение достаточно прямолинейно, но есть нюанс, что **оптимальней использовать int[] вместо Map**.
