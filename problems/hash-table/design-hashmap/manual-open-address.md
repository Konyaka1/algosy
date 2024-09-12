### Solution
_Метод цепочек_. Time: 30:50
```java
class MyHashMap {

    private static final int MAX_TABLE_SIZE = 10001;
    private Entry[] table;

    public MyHashMap() {
        this.table = new Entry[MAX_TABLE_SIZE];
    }

    public void put(int key, int value) {
        int index = hash(key);

        Entry curr = table[index];
        while (curr != null) {
            if (curr.key == key) {
                curr.value = value;
                curr.isDeleted = false;
                return;
            }

            index = nextIndex(index);
            curr = table[index];
        }

        table[index] = new Entry(key, value);
    }

    public int get(int key) {
        int index = search(key);
        if (index != -1 && !table[index].isDeleted) {
            return table[index].value;
        }
        return -1;
    }

    public void remove(int key) {
        int index = search(key);
        if (index != -1) {
            table[index].isDeleted = true;
        }
    }

    private int search(int key) {
        int index = hash(key);

        Entry curr = table[index];
        while (curr != null) {
            if (curr.key == key && !curr.isDeleted) {
                return index;
            }

            index = nextIndex(index);
            curr = table[index];
        }

        return -1;
    }

    private int nextIndex(int index) {
        // linear step
        return (index + 1) % MAX_TABLE_SIZE;
    }

    private int hash(int key) {
        // made on purpose to have collisions.
        return key % 3000;
    }

    class Entry {
        int key;
        int value;
        boolean isDeleted;

        public Entry(int key, int value) {
            this.key = key;
            this.value = value;
            this.isDeleted = false;
        }
    }
}
```
### Time
O(K) -- где K, максимальное количество коллизий. 
### Memory
O(N) -- где N, количество элементов в мапе.
### Explication
Создаем массив длинной наибольшего кол-ва элементов. Так как операций put может быть 10^4, создаем такой же длины массив.
При вставке, вставляем до тех пор, пока не найдем пустое место. Место ищем с определенным шагом. В данном случае линейным.

**ВАЖНО**: Нельзя просто пометить элемент null при удалении. Потому что это может сломать цепочку. 
Поэтому заводим флаг isDeleted для пометки удаленного элемента.