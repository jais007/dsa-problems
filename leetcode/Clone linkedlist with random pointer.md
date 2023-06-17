```java
static Node copyRandomList(Node head) {
     Node temp = head;
	//step 1
    while(temp != null) {
        Node newNode = new Node(temp.val);
        newNode.next = temp.next;
        temp.next = newNode;
        temp = temp.next.next;
    }
	//step 2
    Node itr = head;
    while(itr != null) {
        if(itr.random != null)
            itr.next.random = itr.random.next;
        itr = itr.next.next;
    }
	//step 3
    Node dummy = new Node(0);
    itr = head;
    temp = dummy;
    Node fast;
    while(itr != null) {
        fast = itr.next.next;
        temp.next = itr.next;
        itr.next = fast;
        temp = temp.next;
        itr = fast;
    }
    return dummy.next;
}
```
