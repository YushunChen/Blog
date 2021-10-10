---
description: ID: 134; hard; LRU缓存策略
---
# LRU Cache

{% embed url="https://www.lintcode.com/problem/134/" %}

{% embed url="https://leetcode.com/problems/lru-cache/" %}

## Solution 1 (Java)

```java
public class LRUCache {

    class Node {
        int key, val;
        Node next = null;

        public Node(int key, int val) {
            this.key = key;
            this.val = val;
            this.next = null;
        }
    }

    int capacity, size;
    Node dummy, end;
    HashMap<Integer, Node> keyToPrevMap;

    /*
     * @param capacity: An integer
     */
    public LRUCache(int capacity) {
        this.capacity = capacity;
        this.size = 0;
        this.dummy = new Node(0, 0);
        this.end = this.dummy;
        this.keyToPrevMap = new HashMap<Integer, Node>();
    }

    /*
     * @param key: An integer
     * @return: An integer
     */
    public int get(int key) {
        if (!keyToPrevMap.containsKey(key))
            return -1;

        moveToEnd(key);
        return end.val;
    }

    /*
     * @param key: An integer
     * @param value: An integer
     * @return: nothing
     */
    public void set(int key, int value) {
        // Case I: replace old key and value
        if (get(key) != -1) {
            Node prev = keyToPrevMap.get(key);
            prev.next.val = value;
            return;
        }

        // Case II: add new key and value when in capacility limit
        if (size < capacity) {
            Node newNode = new Node(key, value);
            end.next = newNode;
            keyToPrevMap.put(key, end);
            end = newNode;
            size++;
            return;
        }

        // Case III: invalidate LRU item and add new key and value
        // 1. remove first/LRU node
        Node firstNode = dummy.next;
        keyToPrevMap.remove(firstNode.key);
        // 2. reuse that first node and move it to the end
        firstNode.key = key;
        firstNode.val = value;
        keyToPrevMap.put(key, dummy);
        moveToEnd(key);
    }

    private void moveToEnd(int key) {
        Node prev = keyToPrevMap.get(key);
        Node curr = prev.next;

        if (curr == end) return;
        prev.next = curr.next;
        end.next = curr;

        // update the map for prev and curr
        if (prev.next != null) {
            keyToPrevMap.put(prev.next.key, prev);
        }
        keyToPrevMap.put(curr.key, end);
        end = curr;
    }
}
```

### Notes

We uses a singly linked list and a hash map in this solution. The linked list is basically the cache, where the head is the least recently used (LRU) and the end is the most recently used.The hash map keeps track of **key** and **previous node** pairs.

* We first define a `Node` class with fields including `key`, `val`, and `next`.
* Then, the fields of the `LRUCache` class includes:
  * `capacity`: the full capacity of the cache as required by user input.
  * `size`: the current size of the cache
  * `dummy`: the dummy node pointing to the head of the linked list
  * `end`: the end of the linked list
  * `keyToPrevMap`: the hash map of `(key, previous node)` pairs.

#### The `get` method

We first check if a node with the input `key` is in the map. If not, we return -1 not found. If we do find a node associated with that key, we move that node to the end of the linked list and return its value. (`moveToEnd` method to be completed later)

#### The `set` method

We have three cases for setting key/value pairs.

1. The key is already contained in the map. All we need to do is find that node and change its value.
2. Within in the capacity limit, we can directly add a new node to the end of the linked list. Do not forget to update the `end`, the `map`, and the `size`.
3. When the capacity limit will be exceeded, we remove the first/LRU node from the `map`. Next, we reuse that first node by putting the new key and value into that node. Then, we move that node to the end of the linked list, meaning that it is the most recently used. Do not forget to update the map as well (for changing the head of the list).

#### The `moveToEnd` method

We take in a `key` and want to move the node associated with that key to the end of the linked list. We first remove it from where it currently is, i.e., pointing its previous node to its next node. Then, we add it at the end of the list. More importantly, do not forget to update the `map` since two positions in the linked list have changed and do not forget to update end as well.

## Solution 2 (Java)

```java
class LRUCache {
    
    class Node {
        int key, val;
        Node prev, next;
        public Node(int key, int val) {
            this.key = key;
            this.val = val;
            this.prev = null;
            this.next = null;
        }
    }
    
    int capacity;
    Node head, tail;
    Map<Integer, Node> map;

    public LRUCache(int capacity) {
        this.capacity = capacity;
        head = new Node(-1, -1);
        tail = new Node(-1, -1);
        head.next = tail;
        tail.prev = head;
        this.map = new HashMap<>();
    }
    
    public int get(int key) {
        if (!map.containsKey(key))
            return -1;
        Node curr = map.get(key);
        curr.prev.next = curr.next;
        curr.next.prev = curr.prev;
        moveToTail(curr);
        return curr.val;
    }
    
    public void put(int key, int value) {
        if (get(key) != -1) {
            Node curr = map.get(key);
            curr.val = value;
            return;
        }
        
        if (map.size() == capacity) {
            map.remove(head.next.key);
            head.next = head.next.next;
            head.next.prev = head;
        }
        
        Node newNode = new Node(key, value);
        map.put(key, newNode);
        moveToTail(newNode);
    }
    
    private void moveToTail(Node curr) {
        curr.prev = tail.prev;
        tail.prev = curr;
        curr.prev.next = curr;
        curr.next = tail;
    }
}

// O <-> O <-> O <-> O <-> O

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache obj = new LRUCache(capacity);
 * int param_1 = obj.get(key);
 * obj.put(key,value);
 */
```

### Notes

* Here we used a doubly linked list.
* Note that `head` and `tail` are not actually the head and tail of the doubly linked list. `Head` is the node before the actual head and `tail` is the node after the actual tail of the list.
