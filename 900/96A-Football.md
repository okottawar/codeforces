# Question 96A - Football

## Problem

Given a string consisting of only `0` and `1`, determine whether there exists a contiguous group of at least `7` identical characters.

* Print `YES` if such a group exists
* Otherwise print `NO`

---

## Initial Thought Process

* We need to check consecutive characters.
* A fixed window of size `7` is enough.
* If all characters inside a window are the same, answer becomes `YES`.

---

## Insight

* Any dangerous situation must appear inside some substring of length `7`.
* For every window:

  * either all characters are `0`
  * or all characters are `1`
* The moment we find one valid window, we can stop immediately.

---

## Algorithm

```text
READ string s

FOR every window of size 7
    SET allZero = true
    SET allOne = true

    FOR each character inside the window
        IF character != '0'
            allZero = false

        IF character != '1'
            allOne = false

    IF allZero OR allOne
        PRINT "YES"
        STOP

PRINT "NO"
```

---

## Edge Cases

* String length less than `7` → always `NO`
* Exactly `7` equal characters → `YES`
* Multiple groups present → first valid window is enough
* Alternating characters like `1010101` → `NO`

---

## Time and Space Complexity

* **Time Complexity:** `O(n)`
* **Space Complexity:** `O(1)`

---

## Java Code

```java
import java.io.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String s = br.readLine();

        for (int i = 0; i <= s.length() - 7; i++) {

            boolean allZero = true;
            boolean allOne = true;

            for (int j = i; j < i + 7; j++) {
                if (s.charAt(j) != '0') {
                    allZero = false;
                }
                if (s.charAt(j) != '1') {
                    allOne = false;
                }
            }

            if (allZero || allOne) {
                System.out.println("YES");
                return;
            }
        }

        System.out.println("NO");
    }
}
```
