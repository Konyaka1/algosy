### Solution
_Метод цепочек_. Time: 14:20.
```java
class MyHashMap {

    private static final int DEFAULT_BUCKETS_SIZE = 16;
    private List<Entry>[] table;

    public MyHashMap() {
        this.table = new List[DEFAULT_BUCKETS_SIZE];
        for (int i = 0; i < DEFAULT_BUCKETS_SIZE; i++) {
            this.table[i] = new LinkedList<>();
        }
    }

    public void put(int key, int value) {
        int index = bucketIndex(key);
        List<Entry> chain = table[index];

        for (Entry pair : chain) {
            if (pair.key == key) {
                pair.value = value;
                return;
            }
        }

        chain.add(new Entry(key, value));
    }

    public int get(int key) {
        int index = bucketIndex(key);
        List<Entry> chain = table[index];

        for (Entry pair : chain) {
            if (pair.key == key) {
                return pair.value;
            }
        }
        return -1;
    }

    public void remove(int key) {
        int index = bucketIndex(key);
        List<Entry> chain = table[index];

        chain.removeIf(entry -> entry.key == key);
    }


    private int bucketIndex(int keyHash) {
        return keyHash % DEFAULT_BUCKETS_SIZE;
    }

    class Entry {
        int key;
        int value;

        public Entry(int key, int value) {
            this.key = key;
            this.value = value;
        }
    }
}
```
### Time
O(K) -- где K, максимальное количество коллизий. 
### Memory
O(N) -- где N, количество элементов в мапе.
### Explication
Создаем массив цепочек (chain). Индекс массива равен остатку от деления на размера массива.
Далее тривиально итерируем через каждую цепочку и делаем сравнения по ключу.