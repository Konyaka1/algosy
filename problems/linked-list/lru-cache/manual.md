### Solution. Interview solution
```java
class LRUCache {

    private final int capacity;
    private final Map<Integer, Node> map;
    private final Node head;
    private final Node tail;

    public LRUCache(int capacity) {
        this.map = new HashMap<>(capacity * 3);
        this.capacity = capacity;

        this.head = new Node(-1, -1);
        this.tail = new Node(-1, -1);

        this.head.next = this.tail;
        this.tail.prev = this.head;
    }

    public int get(int key) {
        Node val = this.map.get(key);
        if (val == null) {
            return -1;
        }

        this.removeNode(val);
        this.addNode(val);

        return val.val;
    }

    public void put(int key, int val) {
        Node old = this.map.get(key);
        if (old != null) {
            this.map.remove(key);
            this.removeNode(old);
        }

        Node newNode = new Node(key, val);
        this.map.put(key, newNode);
        this.addNode(newNode);

        if (this.map.size() > capacity) {
            Node nodeToDelete = this.tail.prev;
            this.map.remove(nodeToDelete.key);
            this.removeNode(nodeToDelete);
        }
    }

    private void addNode(Node node) {
        Node curHead = this.head.next;
        this.head.next = node;
        node.prev = this.head;

        node.next = curHead;
        curHead.prev = node;
    }

    private void removeNode(Node node) {
        Node next = node.next;
        Node prev = node.prev;

        next.prev = prev;
        prev.next = next;
    }

    class Node {
        int key;
        int val;
        Node prev;
        Node next;

        public Node(int key, int val) {
            this.key = key;
            this.val = val;
        }
    }
}
```
### Solution. Own hash map with open address (fastest)
```java
class LRUCache {

    private final Node[] table;
    private int size;
    private final int capacity;

    private final Node head;
    private final Node tail;

    public LRUCache(int capacity) {
        this.table = new Node[capacity * 5];
        this.capacity = capacity;

        this.head = new Node(-1, -1);
        this.tail = new Node(-1, -1);

        this.head.next = this.tail;
        this.tail.prev = this.head;
    }

    public int get(int key) {
        int bucket = this.search(key);
        if (bucket == -1) {
            return -1;
        }

        Node tmp = this.table[bucket];
        this.removeNode(tmp);
        this.addToTop(tmp);

        return tmp.val;
    }

    public void put(int key, int val) {
        this.remove(key);

        this.addPair(key, val);

        this.removeOld();
    }

    private void remove(int key) {
        int bucket = this.search(key);
        if (bucket == -1) {
            return;
        }
        Node node = this.table[bucket];

        this.removeNode(node);
        node.deleted = true;
        size--;
    }

    private void removeOld() {
        if (size <= capacity) {
            return;
        }

        this.remove(this.tail.prev.key);
    }

    private void addPair(int key, int val) {
        int i = 0;
        while (true) {
            int bucket = this.bucket(key, i);
            Node tmp = this.table[bucket];
            if (tmp == null || tmp.deleted) {
                Node newNode = new Node(key, val);
                this.table[bucket] = newNode;
                size++;

                this.addToTop(newNode);
                return;
            }
            i++;
        }
    }

    private int search(int key) {
        int i = 0;

        while (true) {
            int bucket = this.bucket(key, i);
            Node tmp = this.table[bucket];
            if (tmp == null || tmp.deleted) {
                return -1;
            }
            if (tmp.key == key) {
                return bucket;
            }
            i++;
        }
    }

    private void addToTop(Node node) {
        Node oldHead = this.head.next;
        this.head.next = node;
        node.prev = this.head;

        node.next = oldHead;
        oldHead.prev = node;
    }

    private void removeNode(Node node) {
        Node prev = node.prev;
        Node next = node.next;

        prev.next = next;
        next.prev = prev;
    }

    private int bucket(int key, int step) {
        return (key + step * step) % this.table.length;
    }

    class Node {
        int key;
        int val;
        Node prev;
        Node next;
        boolean deleted;

        public Node(int key, int val) {
            this.key = key;
            this.val = val;
        }
    }
}
```

### Solution. Own hash map with open chains
```java
class LRUCache {

    private final List<Node>[] table;
    private final int capacity;
    private int size;
    private Node head;
    private Node tail;

    public LRUCache(int capacity) {
        this.table = new List[capacity];

        for (int i = 0; i < table.length; i++) {
            table[i] = new LinkedList<Node>();
        }

        this.capacity = capacity;
        this.head = new Node(0, 0);
        this.tail = new Node(0, 0);

        this.head.next = this.tail;
        this.tail.prev = this.head;
    }

    public int get(int key) {
        int i = this.index(key);

        for (Node node : table[i]) {
            if (node.key == key) {
                // mark as new
                removeNode(node);
                addHead(node);
                return node.val;
            }
        }

        return -1;
    }

    public void put(int key, int value) {
        int i = this.index(key);

        for (Node node : table[i]) {
            if (node.key == key) {
                // mark as new
                removeNode(node);
                addHead(node);
                node.val = value;
                return;
            }
        }

        if (size == capacity) {
            // evict oldest
            Node lru = removeTail();
            int lruKeyIndex = this.index(lru.key);

            table[lruKeyIndex].removeIf((node) -> node.key == lru.key);
        } else {
            size++;
        }
        Node tmp = new Node(key, value);
        table[i].add(tmp);
        addHead(tmp);
    }


    private void removeNode(Node node) {
        Node prev = node.prev;
        Node next = node.next;

        prev.next = next;
        next.prev = prev;
    }

    private void addHead(Node node) {
        Node curHead = head.next;
        head.next = node;
        node.prev = head;
        node.next = curHead;
        curHead.prev = node;
    }

    private Node removeTail() {
        Node curTail = tail.prev;
        Node prev = curTail.prev;
        prev.next = tail;
        tail.prev = prev;

        return curTail;
    }

    private int index(int key) {
        return key % table.length;
    }

    class Node {
        int key;
        int val;
        Node prev;
        Node next;

        public Node(int key, int val) {
            this.key = key;
            this.val = val;
        }
    }
}
```
### Solution. Shortest one
```java
class LRUCache {

    private final Map<Integer, Integer> map;
    private final int cap;

    public LRUCache(int capacity) {
        this.cap = capacity;
        this.map = new LinkedHashMap<>(capacity * 2, 0.99f, true) {
            @Override
            private boolean removeEldestEntry(Map.Entry<Integer, Integer> eldest) {
                return size() > cap;
            }
        };
    }
    
    public int get(int key) {
        return this.map.getOrDefault(key, -1);
    }
    
    public void put(int key, int value) {
        this.map.put(key, value);
    }
}
```
### Time
O(1) -- Для всех операций
### Memory
O(1) -- Для всех операций
### Explication
Используем обычную мапу, независимо от реализации. Важно хранить связи между
элементами используя двух-связный список. При удалении элемента, удаляем связи.
При добавлении или при обращении -- переносим элемент в начало.
