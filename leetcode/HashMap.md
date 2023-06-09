### HashMap

```java

class MyHashMap {
 private final int mult = 12582917
public:
    int SIZE = 1e6;
   
    ListNode[] table;
    
    MyHashMap() {
        this.table = new ListNode[SIZE];
    }

    private int hash(int key){
        return (int)((long) key * multi % SIZE);
    } 

    void put(int key, int value) {
        int hashCode = hash(key);
        ListNode node = table[hashCode];
        ListNode newNode = new ListNode(key, value);
        if(node == null){
            table[hashCode] = newNode;
        }else{
            ListNode previousNode = null;
            while(node != null){
                if(node.key == key){
                    node.value = value;
                    return;
                }
                previousNode = node;
                node = node.next;
            }
            previousNode.next = newNode;
        }
    }
    
    int get(int key) {
        int hashCode = hash(key);
        ListNode node = table[hashCode];
        if(node == null){
            return -1;
        }else{
            while(node != null){
                if(node.key == key){
                    return node.value;
                }
                node = node.next;
            }
        }
       return -1;
    }
    
    void remove(int key) {
        int hashCode = hash(key);
        ListNode node = table[hashCode];
        if(node == null){
            return;
        }else{
            ListNode prev = null;
            while(node != null){
                if(node.key == key){
                    prev.next = node.next;
                    return;
                }
                prev = node;
                node = node.next;
            }
        }
    }

    class ListNode {
        int key, val;
        ListNode next;
        public ListNode(int key, int val) {
            this.key = key;
            this.val = val;
        }
    }
};

/**
 * Your MyHashMap object will be instantiated and called as such:
 * MyHashMap* obj = new MyHashMap();
 * obj->put(key,value);
 * int param_2 = obj->get(key);
 * obj->remove(key);
 */
 ```