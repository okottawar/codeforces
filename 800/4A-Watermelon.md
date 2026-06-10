# Question 4A - Watermelon

## Problem

Given an integer W, determine whether it can be split into two **positive even integers** whose sum is W.

---

## Initial Thought Process

* Even numbers might be splittable into two even parts.
* Odd numbers immediately seem impossible since even + even = even.
* Need to verify smallest even cases.

---

## Insight

* Odd numbers cannot be written as sum of two even numbers.
* Any even number ≥ 4 works:
  * Example: 4 = 2 + 2, 6 = 2 + 4, 8 = 4 + 4
* The only failure case is W = 2.

---

## Algorithm

```
IF W % 2 == 0 AND W > 2
    PRINT "YES"
ELSE
    PRINT "NO"
```

---

## Edge Cases

* W = 1 → NO
* W = 2 → NO (smallest even number but invalid)
* W = 3 → NO (odd)
* W = 4 → YES (first valid case)

---

## Time and Space Complexity

* **Time Complexity:** `O(1)`
* **Space Complexity:** `O(1)`

---

## Java Code

```java
import java.io.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int w = Integer.parseInt(br.readLine());

        if (w % 2 == 0 && w > 2) {
            System.out.println("YES");
        } else {
            System.out.println("NO");
        }
    }
}
```
