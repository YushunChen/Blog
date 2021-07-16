---
description: 'ID: 1; naive'
---

# A + B Problem

{% embed url="https://www.lintcode.com/problem/1/" %}

## Solution 1 \(Java\)

```java
public class Solution {
    /**
     * @param a: An integer
     * @param b: An integer
     * @return: The sum of a and b 
     */
    public int aplusb(int a, int b) {
        return a + b;
    }
}
```

## Solution 2 \(Java\)

```java
public class Solution {
    /**
     * @param a: An integer
     * @param b: An integer
     * @return: The sum of a and b 
     */
    public int aplusb(int a, int b) {
        while (b != 0) {
            int aTemp = a ^ b;
            int bTemp = (a & b) << 1;
            a = aTemp;
            b = bTemp;
        }
        return a;
    }
}
// ADD
// 1110 = 14
// 1011 = 11
//11001 = 25

// XOR (不进位加法)
// 1110   00101   10001   a
// 1011   10100   01000   b
// 0101   10001   11001   a ^ b

// AND
// 1110   00101   10001   a
// 1011   10100   01000   b
// 1010   00100   00000   a & b

// a = 1110,  0101, 10001, 11001
// b = 1011, 10100, 01000, 00000
```

### Notes

In order to avoid using the plus sign in this problem, we can use the XOR operation \(if two digits are different, the result is 1; otherwise, the result is 0. The XOR operation is essentially adding without carrying. Thus, we can first XOR the two numbers and then add the carry bits. 

{% hint style="info" %}
This means `a + b = (a ^ b) + (a & b << 1)`
{% endhint %}

Eventually, the carry bits are zeros \(`b == 0`\) and we end the operation. Example of tracing the code is shown above. We have 14 + 11 = 25, or in binary: 1110 + 1011 = 11011.

### Citation

{% embed url="https://www.lintcode.com/problem/1/solution/29459" %}

