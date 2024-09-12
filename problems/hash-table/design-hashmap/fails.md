## Fails
1st try для метода цепочек

### Open address
[LOGIC] Wrong answer. Нельзя просто пометить элемент null, потому что может разрушиться цепочка.
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
                return;
            }

            index = nextIndex(index);
            curr = table[index];
        }

        table[index] = new Entry(key, value);
    }
    
    public int get(int key) {
        int index = search(key);
        if (index != -1) {
            return table[index].value;
        }
        return -1;
    }
    
    public void remove(int key) {
        int index = search(key);
        if (index != -1) {
            table[index] = null;
        }
    }

    private int search(int key) {
        int index = hash(key);
        
        Entry curr = table[index];
        while (curr != null) {
            if (curr.key == key) {
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
        return key % 1000;
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