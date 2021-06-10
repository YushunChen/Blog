---
description: 'ID: 134; hard; LRU缓存策略'
---

# TODO: LRU Cache

{% embed url="https://www.lintcode.com/problem/134/" %}

## Solution 1 \(Java\)

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
    */public LRUCache(int capacity) {
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

