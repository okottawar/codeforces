# Question 112A - Petya and Strings

## Problem

Compare two strings lexicographically (case-insensitive) and print:

* `1` if first string is greater
* `-1` if first string is smaller
* `0` if both are equal

---

## Initial Thought Process

* Convert both strings to lowercase.
* Compare characters from left to right.
* Decide based on the first mismatch.

---

## Insight

* Lexicographical order depends only on the **first differing character**.
* If all characters match, strings are equal.
* No need to compare full sums or entire strings once a difference is found.

---

## Algorithm

```text
READ first, second
CONVERT both strings to lowercase

FOR i from 0 to length-1
    IF first[i] > second[i]
        PRINT 1
        STOP
    ELSE IF first[i] < second[i]
        PRINT -1
        STOP

PRINT 0
```

---

## Edge Cases

* Strings are identical → output `0`
* Difference at first character → immediate decision
* Case differences only → treated as equal after lowercase conversion

---

## Time and Space Complexity

* **Time Complexity:** `O(n)` (stops early on first mismatch)
* **Space Complexity:** `O(1)`

---

## Java Code

```java
import java.io.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        String first = br.readLine().toLowerCase();
        String second = br.readLine().toLowerCase();

        for (int i = 0; i < first.length(); i++) {
            if (first.charAt(i) > second.charAt(i)) {
                System.out.println(1);
                return;
            } else if (first.charAt(i) < second.charAt(i)) {
                System.out.println(-1);
                return;
            }
        }

        System.out.println(0);
    }
}
```
