## Fails
#### 1st error
[SYNTAX] Map is not iterable itself. We need to call **entrySet()**
```java
class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        Map<Integer, Integer> freqMap = new HashMap<>();

        for (int num : nums) {
            freqMap.merge(num, 1, Integer::sum);
        }

        List<List<Integer>> invertedFreq = new ArrayList<>(nums.length - 1);
        for (int i = 0; i < nums.length - 1; i++) {
            invertedFreq.add(new LinkedList<Integer>());
        }


        for (Map.Entry<Integer, Integer> entry : freqMap) {
            int num = entry.getKey();
            int freq = entry.getValue();

            List<Integer> numsWithFreq = invertedFreq.get(freq - 1);
            numsWithFreq.add(num);
        }

        List<Integer> result = new ArrayList<>(k);

        for (int i = nums.length - 2; i >= 0; i--) {
            List<Integer> numsWithFreq = invertedFreq.get(i);

            result.addAll(numsWithFreq);
            k = k - numsWithFreq.size();
            if (k == 0) {
                break;
            }
        }

        return result.stream().mapToInt(e -> e).toList();
    }
}
```

#### 2nd error

[SYNTAX] IntStream doesn't have toList() method. Moreover I have to return array.
```java
class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        Map<Integer, Integer> freqMap = new HashMap<>();
        
        for (int num : nums) {
            freqMap.merge(num, 1, Integer::sum);
        }
        
        List<List<Integer>> invertedFreq = new ArrayList<>(nums.length - 1);
        for (int i = 0; i < nums.length - 1; i++) {
            invertedFreq.add(new LinkedList<Integer>());
        }
        
        
        for (Map.Entry<Integer, Integer> entry : freqMap.entrySet()) {
            int num = entry.getKey();
            int freq = entry.getValue();
            
            List<Integer> numsWithFreq = invertedFreq.get(freq - 1);
            numsWithFreq.add(num);    
        }
        
        List<Integer> result = new ArrayList<>(k);
        
        for (int i = nums.length - 2; i >= 0; i--) {
            List<Integer> numsWithFreq = invertedFreq.get(i);
            
            result.addAll(numsWithFreq);
            k = k - numsWithFreq.size();
            if (k == 0) {
                break;   
            }            
        }
        
        return result.stream().mapToInt(e -> e).toList();
    }
}
```
#### 3rd error
[LOGIC] Index 0 out of bounds for length 0. 

Почему-то я в моей голове invertedFreq должен был хранить на 1 меньше элементов, час самих элементов. Мда
```java
class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        Map<Integer, Integer> freqMap = new HashMap<>();
        
        for (int num : nums) {
            freqMap.merge(num, 1, Integer::sum);
        }
        
        List<List<Integer>> invertedFreq = new ArrayList<>(nums.length - 1);
        for (int i = 0; i < nums.length - 1; i++) {
            invertedFreq.add(new LinkedList<Integer>());
        }
        
        
        for (Map.Entry<Integer, Integer> entry : freqMap.entrySet()) {
            int num = entry.getKey();
            int freq = entry.getValue();
            
            List<Integer> numsWithFreq = invertedFreq.get(freq - 1);
            numsWithFreq.add(num);    
        }
        
        List<Integer> result = new ArrayList<>(k);
        
        for (int i = nums.length - 2; i >= 0; i--) {
            List<Integer> numsWithFreq = invertedFreq.get(i);
            
            result.addAll(numsWithFreq);
            k = k - numsWithFreq.size();
            if (k == 0) {
                break;   
            }            
        }
        
        return result.stream().mapToInt(e -> e).toArray();
    }
}
```

## 2nd attempt
[SYNTAX] Пересечение в наименовании переменных. **freq** 
```java
class Solution {
    public int[] topKFrequent(int[] nums, int k) {

        Map<Integer, Integer> freq = new HashMap<>();

        for (int num : nums) {
            freq.merge(num, 1, Integer::sum);
        }
        List<Integer>[] reversedFreq = new List[nums.length];


        
        for (int i = 0; i < nums.length; i++) {
            reversedFreq[i] = new LinkedList<>();
        }


        for (Map.Entry<Integer, Integer> entry : freq.entrySet()) {
            Integer num = freq.getKey(); 
            int freq = freq.getValue(); 

            reversedFreq[freq - 1].add(num); 
        }

        List<Integer> result = new LinkedList<>();

        for (int i = nums.length - 1; i >= 0 && k > 0; i--) { 
            List<Integer> topIElements = reversedFreq[i];
            result.addAll(topIElements);
            k = k - topIElements.size(); 
        }

        return result.stream().mapToInt(e -> e).toArray();

    }
}
```