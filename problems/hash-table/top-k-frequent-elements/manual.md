### Solution

```java
class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        Map<Integer, Integer> freqMap = new HashMap<>();

        for (int num : nums) {
            freqMap.merge(num, 1, Integer::sum);
        }

        List<List<Integer>> invertedFreq = new ArrayList<>(nums.length - 1);
        for (int i = 0; i < nums.length; i++) {
            invertedFreq.add(new LinkedList<Integer>());
        }

        for (Map.Entry<Integer, Integer> entry : freqMap.entrySet()) {
            int num = entry.getKey();
            int freq = entry.getValue();

            List<Integer> numsWithFreq = invertedFreq.get(freq - 1);
            numsWithFreq.add(num);
        }

        List<Integer> result = new ArrayList<>(k);

        for (int i = nums.length - 1; i >= 0; i--) {
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

### Time
O(N) -- Потому что проходим через весь array.
### Memory
O(N) -- Потому что храним весь мапу, где ключи это все уникальные значения

### Explication
Сначала мы собираем все элементы по принципу "элемент -> кол-во повторений"

Затем мы группируем элементы по количеству повторений и получаем следующую мапу "кол-во повторений -> элемент". 
Важно, группа должна быть отсортированной, то есть по ней нужно будет итерировать

Последним действием проходим по группе в обратном порядке и собираем результат 
### Note
#### Syntax improvements
При инициализировании каждого элемента в invertedFreq, не обязательно указывать тип LinkedList, 
потому что тип известен еще на компиляции
```java
List<List<Integer>> invertedFreq = ...

invertedFreq.add(new LinkedList<>());
```