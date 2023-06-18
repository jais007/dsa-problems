```java
class Node{
    int key, val;
    Node next, prev;

    Node(int key, int val){
        this.key = key;
        this.val = val;
    }
}
class LRUCache {
    int capacity; 
    HashMap<Integer, Node> cache;
    Node head, tail;

    public LRUCache(int capacity) {
        this.capacity = capacity;
        cache = new HashMap<>();
        head = new Node(-1,-1);
        tail = new Node(-1,-1);
        head.next = tail;
        tail.prev = head;
    }
    
    public int get(int key) {
        //check if exist 
        if(cache.containsKey(key)){
            //update the list and hashmap
            Node node = cache.get(key);
            remove(node);
            insert(node);
            return node.val;
        }
        return -1;          
    }
    
    public void put(int key, int value) {
        //check if exist then remove that and insert new node?
        if(cache.containsKey(key)){
            remove(cache.get(key));
        }
        // //remove LRU node if size is full
        if(capacity == cache.size()){
            
            remove(tail.prev);
        }
         //insert new Node
        insert(new Node(key, value));
    }

    private void insert(Node node){
        cache.put(node.key, node);
        node.next = head.next;
        node.next.prev = node;
        node.prev = head;
        head.next = node;
    }
    private void remove(Node node){
        cache.remove(node.key);
        node.prev.next = node.next;
        node.next.prev = node.prev;
    }
}


/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache obj = new LRUCache(capacity);
 * int param_1 = obj.get(key);
 * obj.put(key,value);
 */
```
