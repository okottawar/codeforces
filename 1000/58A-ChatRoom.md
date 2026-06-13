# Question 58A - Chat room

## Problem

Given a string `s`, determine whether the word **"hello"** appears as a subsequence inside it.

A subsequence means:

* Characters appear in order
* But not necessarily consecutively

Example:

* `"ahhellllloou"` → YES
* `"hlelo"` → NO

---

## Initial Thought Process

* We need to check if we can match the characters of `"hello"` in order.
* We scan the input string from left to right.
* Whenever a character matches the current required character, we move forward in `"hello"`.

---

## Insight

* This is a **subsequence matching problem**.
* We do NOT need to modify the input string.
* Greedy matching works because order is fixed.
* Once a character of `"hello"` is matched, we move to the next one.

---

### Algorithm

```text id="alg58a"
SET target = "hello"
INITIALIZE index = 0

FOR each character c in input string:
    IF c == target[index]:
        index++

    IF index == length of target:
        PRINT "YES"
        STOP

PRINT "NO"
```

---

## Edge Cases

* String shorter than `"hello"` → always NO
* Repeated letters → still valid if order is preserved
* Characters in correct order but spaced out → valid
* Missing any required character → NO

---

## Time and Space Complexity

* **Time Complexity:** `O(n)` - single pass through string
* **Space Complexity:** `O(1)` - only index tracking used

---

## Java Code

```java id="code58a"
import java.io.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String s = br.readLine();

        String target = "hello";
        int j = 0;

        for (int i = 0; i < s.length(); i++) {
            if (s.charAt(i) == target.charAt(j)) {
                j++;
            }
            if (j == target.length()) {
                System.out.println("YES");
                return;
            }
        }

        System.out.println("NO");
    }
}
```
