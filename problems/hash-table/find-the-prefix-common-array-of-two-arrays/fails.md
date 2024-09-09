## Fails
#### 1st error
[SYNTAX] **C** ??? я это result назвал емае
```java
class Solution {
    public int[] findThePrefixCommonArray(int[] A, int[] B) {
        Set<Integer> setA = new HashSet<>();
        Set<Integer> setB = new HashSet<>();

        int[] result = new int[A.length];

        result[0] = A[0] == B[0];
        setA.add(B[0]);
        setB.add(A[0]);

        for (int i = 1; i < C.length - 2; i++) {
            int ai = A[i];
            int bi = B[i];
            result[i] = result[i - 1] + setA.contains(bi) + setB.contains(ai) + (ai == bi);
        }

        result[c.length - 1] = c.length;

        return result;
    }
}
```
#### 2nd error
[SYNTAX] Почему я только в одном месте подправил C ????
```java
class Solution {
    public int[] findThePrefixCommonArray(int[] A, int[] B) {
        Set<Integer> setA = new HashSet<>();
        Set<Integer> setB = new HashSet<>();
        
        int[] result = new int[A.length];
        
        result[0] = A[0] == B[0] ? 1 : 0;
        setA.add(B[0]);
        setB.add(A[0]);
        
        for (int i = 1; i < result.length - 2; i++) {
            int ai = A[i];
            int bi = B[i];
            result[i] = result[i - 1] + (setA.contains(bi) ? 1 : 0) + (setB.contains(ai) ? 1 : 0) + (ai == bi ? 1 : 0);    
        }
        
        result[c.length - 1] = c.length;
        
        return result;
    }
}
```
#### 3rd error
[LOGIC] Почему result.length - 2 ??????
```java
class Solution {
    public int[] findThePrefixCommonArray(int[] A, int[] B) {
        Set<Integer> setA = new HashSet<>();
        Set<Integer> setB = new HashSet<>();

        int[] result = new int[A.length];

        result[0] = A[0] == B[0] ? 1 : 0;
        setA.add(B[0]);
        setB.add(A[0]);

        for (int i = 1; i < result.length - 2; i++) {
            int ai = A[i];
            int bi = B[i];

            result[i] = result[i - 1] + (setA.contains(bi) ? 1 : 0) + (setB.contains(ai) ? 1 : 0) + (ai == bi ? 1 : 0);

            setA.add(bi);
            setB.add(ai);
        }

        result[result.length - 1] = result.length;

        return result;
    }
}
```
#### 4th error
[LOGIC] Почему я добавляю посещенные элементы в противолопожные сеты???
```java
class Solution {
    public int[] findThePrefixCommonArray(int[] A, int[] B) {
        Set<Integer> setA = new HashSet<>();
        Set<Integer> setB = new HashSet<>();

        int[] result = new int[A.length];

        result[0] = A[0] == B[0] ? 1 : 0;
        setA.add(B[0]);
        setB.add(A[0]);

        for (int i = 1; i < result.length - 1; i++) {
            int ai = A[i];
            int bi = B[i];

            result[i] = result[i - 1] + (setA.contains(bi) ? 1 : 0) + (setB.contains(ai) ? 1 : 0) + (ai == bi ? 1 : 0);

            setA.add(bi);
            setB.add(ai);
        }

        result[result.length - 1] = result.length;

        return result;
    }
}
```