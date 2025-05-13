### Solution
```go
func topKFrequent(nums []int, k int) []int {
    freq := make(map[int]int)
    
    for _, num := range nums {
        freq[num]++
    }
    
    countFreq := make([][]int, len(nums) + 1)
    
    for k, v := range freq {
        countFreq[v] = append(countFreq[v], k)
    }
    
    res := make([]int, 0, k)
    
    for i := len(countFreq) - 1; i > 0 && len(res) < k; i-- {
        frequent := countFreq[i]
        
        res = append(res, frequent...)
    }
    
    return res
}
```

Time: 20:31
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
            Integer num = entry.getKey();
            int count = entry.getValue();

            reversedFreq[count - 1].add(num);
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