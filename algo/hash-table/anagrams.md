---
description: ID: 171; medium
---
# Anagrams

{% embed url="https://www.lintcode.com/problem/171/" %}

## Solution 1 (Java)

```java
public class Solution {
    /**
     * @param strs: A list of strings
     * @return: A list of strings
     */
    public List<String> anagrams(String[] strs) {
        List<String> res = new ArrayList<>();
        Map<String, List<String>> map = new HashMap<>();
        for (String s : strs) {
            char[] sArr = s.toCharArray();
            Arrays.sort(sArr);
            String sSorted = new String(sArr);
            map.putIfAbsent(sSorted, new ArrayList<String>());
            map.get(sSorted).add(s);
        }
        for (List<String> list : map.values()) {
            if (list.size() > 1)
                res.addAll(list);
        }
        return res;
    }

}
```
