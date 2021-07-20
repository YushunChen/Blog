---
description: 'ID: 612; medium'
---

# K Closest Points

{% embed url="https://www.lintcode.com/problem/612/" %}

## Solution 1 \(Java\)

```java
/**
 * Definition for a point.
 * class Point {
 *     int x;
 *     int y;
 *     Point() { x = 0; y = 0; }
 *     Point(int a, int b) { x = a; y = b; }
 * }
 */

public class Solution {
    /**
     * @param points: a list of points
     * @param origin: a point
     * @param k: An integer
     * @return: the k closest points
     */
    public Point[] kClosest(Point[] points, Point origin, int k) {
        if (points == null || points.length < k)
            return new Point[0];
        
        Queue<Point> maxheap = new PriorityQueue<>(k, new Comparator<Point>() {
            public int compare(Point p1, Point p2) {
                int diff = dist(origin, p1) - dist(origin, p2);
                if (diff != 0)
                    return diff;
                if (p1.x != p2.x)
                    return p1.x - p2.x;
                return p1.y - p2.y;
            }
        });

        // O(nlogn)
        for (Point p : points) {
            maxheap.offer(p);
        }
        // O(klogn)
        Point[] res = new Point[k];
        for (int i = 0; i < k; i++) {
            res[i] = maxheap.poll();
        }
        return res;
    }

    private int dist(Point p1, Point p2) {
        return (p1.x - p2.x) * (p1.x - p2.x) + (p1.y - p2.y) * (p1.y - p2.y);
    }
}
```

### Notes

* This is the **min heap** solution. The thought process is the most straight-forward.
* Time complexity: `O(nlogn + klogn) = O(nlogn)`

## Solution 2 \(Java\)

```java
/**
 * Definition for a point.
 * class Point {
 *     int x;
 *     int y;
 *     Point() { x = 0; y = 0; }
 *     Point(int a, int b) { x = a; y = b; }
 * }
 */

public class Solution {
    /**
     * @param points: a list of points
     * @param origin: a point
     * @param k: An integer
     * @return: the k closest points
     */
    public Point[] kClosest(Point[] points, Point origin, int k) {
        Queue<Point> pq = new PriorityQueue<>(k, new Comparator<Point>() {
            public int compare(Point p1, Point p2) {
                int diff = dist(origin, p2) - dist(origin, p1);
                if (diff == 0) diff = p2.x - p1.x;
                if (diff == 0) diff = p2.y - p1.y;
                return diff;
            }
        });

        // O(nlogk)
        for (Point p : points) {
            pq.offer(p);
            if (pq.size() > k) pq.poll();
        }
        k = pq.size();
        Point[] res = new Point[k];
        // O(klogk)
        while (!pq.isEmpty()) {
            res[--k] = pq.poll();
        }
        return res;
    }

    private int dist(Point p1, Point p2) {
        return (p1.x - p2.x) * (p1.x - p2.x) + (p1.y - p2.y) * (p1.y - p2.y);
    }
}
```

### Notes

* This is the **max heap** solution. 
* If p2 is larger than p1, return positive values. This gives us a max heap, vice versa.
* Time complexity: `O(nlogk + klogk) = O(nlogk)`. 
  * So, this max heap version is better than the min heap version though the latter is more straight-forward to think about. The reason is clear because `k` is bounded by `n`.
  * Heap is priority queue in Java and we customize the ordering by overriding the `Comparator`. We iterate the whole `points` array and add each point to the priority queue. However, the priority queue only stores the top k closest points, as supposed to the min heap, which essentially sorts the points by their distance to the origin. 
  * Thus, the offer and poll methods actually take `O(logk)` time in this solution because the size of the heap is k.

## Solution 3 \(Java\)

```java

```

### Notes

* This is the **quick select** solution.

