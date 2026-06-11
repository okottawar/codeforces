# Question 339A - Helpful Maths

## Problem

Given a string containing digits `1`, `2`, `3` separated by `'+'`, rearrange the digits in non-decreasing order and output the result in the same format.

---

## Initial Thought Process (My Version)

* Count occurrences of each digit using an array.
* Reconstruct the string in sorted order.
* While building the result, append `"+"` after every digit.
* Finally, remove the last `"+"` character to fix formatting.

---

## Insight

* The problem is not about the original structure, only frequency matters.
* We need digits in sorted order: all `1`s, then `2`s, then `3`s.
* The key difficulty is correct formatting of `"+"` separators.

---

## Optimized Version (Key Idea)

Instead of building and then fixing the last `"+"`, control when `"+"` is added.

### Key Principle

> Add `"+"` only **between elements**, not after every element.

### Approach

* Track whether we are printing the first element.
* For every next element, prepend `"+"` before printing the digit.
* This avoids the need for post-processing.

### Algorithm

```text id="alg339a"
READ input string

COUNT frequency of 1, 2, 3

SET first = true

FOR each digit in order (1 → 2 → 3):
    REPEAT frequency times:
        IF not first:
            PRINT "+"
        PRINT digit
        SET first = false
```

---

## Edge Cases

* Only one number → no `"+"` needed
* Already sorted input → output unchanged
* All digits same → no separators except internal logic handles correctly

---

## Time and Space Complexity

* **Time Complexity:** `O(n)`
* **Space Complexity:** `O(1)` (fixed frequency array)

---

## Java Code

```java id="code339a"
import java.io.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        String op = br.readLine();
        int[] counts = new int[3];

        for (int i = 0; i < op.length(); i += 2) {
            if (op.charAt(i) == '1') counts[0]++;
            else if (op.charAt(i) == '2') counts[1]++;
            else counts[2]++;
        }

        StringBuilder sb = new StringBuilder();
        boolean first = true;

        for (int i = 0; i < counts[0]; i++) {
            if (!first) sb.append("+");
            sb.append("1");
            first = false;
        }

        for (int i = 0; i < counts[1]; i++) {
            if (!first) sb.append("+");
            sb.append("2");
            first = false;
        }

        for (int i = 0; i < counts[2]; i++) {
            if (!first) sb.append("+");
            sb.append("3");
            first = false;
        }

        System.out.println(sb.toString());
    }
}
```
