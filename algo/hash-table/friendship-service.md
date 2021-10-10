---
description: ID: 560; easy
---
# Friendship Service

{% embed url="https://www.lintcode.com/problem/560/" %}

## Solution 1 (Java)

```java
public class FriendshipService {

    private Map<Integer, Set<Integer>> followers;
    private Map<Integer, Set<Integer>> followings;
    public FriendshipService() {
        followers = new HashMap<>();
        followings = new HashMap<>();
    }

    /*
     * @param user_id: An integer
     * @return: all followers and sort by user_id
     */
    public List<Integer> getFollowers(int user_id) {
        if (followers.containsKey(user_id)) {
            return new ArrayList<Integer>(followers.get(user_id));
        }
        return new ArrayList<Integer>();
    }

    /*
     * @param user_id: An integer
     * @return: all followings and sort by user_id
     */
    public List<Integer> getFollowings(int user_id) {
        if (followings.containsKey(user_id)) {
            return new ArrayList<Integer>(followings.get(user_id));
        }
        return new ArrayList<Integer>();
    }

    /*
     * @param from_user_id: An integer
     * @param to_user_id: An integer
     * @return: nothing
     */
    public void follow(int to_user_id, int from_user_id) {
        followings.putIfAbsent(from_user_id, new TreeSet<Integer>());
        followings.get(from_user_id).add(to_user_id);

        followers.putIfAbsent(to_user_id, new TreeSet<Integer>());
        followers.get(to_user_id).add(from_user_id);
    }

    /*
     * @param from_user_id: An integer
     * @param to_user_id: An integer
     * @return: nothing
     */
    public void unfollow(int to_user_id, int from_user_id) {
        if (followings.containsKey(from_user_id))
            followings.get(from_user_id).remove(to_user_id);

        if (followers.containsKey(to_user_id))
            followers.get(to_user_id).remove(from_user_id);
    }
}
```

### Notes

* Notice here we used `TreeSet` to make sure the get methods return **sorted** and **unique** results.
* In line 16 and 27, we created an ArrayList from a TreeSet ([Initialization using another Collection](https://www.geeksforgeeks.org/initialize-an-arraylist-in-java/)).
