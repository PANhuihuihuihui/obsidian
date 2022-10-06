---
aliases: [algo 007 ]
tags:
  - linklist
---

## Algo 007 
```java
class Program {
    static class DoublyLinkedList {
        public Node head; 
        public Node tail;
    
        public void setHead(Node node){
            if (head == null) {
                head = node;
                tail = node;
                return;
            }
            insertBefore(head,node);
            
        }
        public void setTail(Node node){
            if (tail == null){
                head = node;
                tail = node;
                return;
            }
            insertAfter(tail,node);

        }
        public void insertBefore(Node node, Node nodeToInsert) {
            // similarly  speciall case 1. only one node 2. before is head
            if(nodeToInsert == head&& nodeToInsert == tail) return;
            remove(nodeToInsert);
            nodeToInsert.next = node;
            nodeToInsert.prev = node.prev;
            if (node.prev == null){
                head = nodeToInsert;
            }else
            [
                node.prev.next =  nodeToInsert; 
            ]

            
        }
        public void insertAfter(Node node, Node nodeToInsert) {
            // special case 1. only one node 2. After is taill
            if(nodeToInsert == head && nodeToInsert == tail){
                // only one node here
                return;
            }
            remove(nodeToInsert);// clear the nod
            nodeToInsert.prev = node;
            nodeToInsert.next = node.next;
            if(node.next == null){
                tail = nodeToInsert;
            }else{
                node.next.prev = nodeToInsert;
            }
            node.next = nodeToInsert;
        }
        public void insertAtPosition(int position, Node nodeToInsert){
            Node tmp = head;
            for(int i=0; i<position,i++){
                tmp = tmp.next;
            }
            insertAfter(tmp,nodeToInsert)
        }
        public void removeNodesWithValue(int value){
            Node node = head;
            while(node!=null ){
                node = node.next;
                if (node.value == value) remove(nodeToRemove);
            }
            remove()
        }
        public void remove(Node node) {
            // 判断是不是头尾；因为头尾是特殊的
            if (node == head) head = head.next; 
            if (node == tail) tail = tail.prev; 
            //做这些之前要 判断是不是null 因为null 没有办法访问。
            if (node.prev != null) node.prev.next = node.next; 
            if (node.next != null) node.next.prev = node.prev;
            // also remember to remove the current pointer to null;
            node.prev = null;
            node.next = null;
            // release memeory ? notify the jvm?

            
        }
        public boolean containsNodeWithValue(int value) {
            Node node = head;
            while(node!=null && node.value != value) node = node.next;
            return node!= null; // good!
        }
        public void removeNodeBindings(Node node) {
            
        }

        static class Node { 
            public int value; 
            public Node prev; 
            public Node next;
            public Node(int value) { 
                this.value = value;
            } 
        }
    }
}

```

#### Takeaways
1.  when add node:  remove the coming node previous link >> connect the comming node first >> carefully connect the original node link;
2. when remvoe node: 判断头尾， 清理link
3. 访问前一定要判断！！！ null 的时候是访问不了的