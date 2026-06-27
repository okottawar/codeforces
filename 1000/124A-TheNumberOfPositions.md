# Question 124A - The number of positions

## Problem

There are `n` people standing in a line.

Find the number of possible positions for a person such that:

* At least `a` people stand in front of them.
* At most `b` people stand behind them.

Print the number of valid positions.

---

## Initial Thought Process

* A position is valid only if it satisfies **both** conditions.
* Instead of checking every position, derive the range of valid positions mathematically.
* Convert each condition into a bound on the person's position.

---
## Insight

Let the person's position (1-indexed) be `pos`.

From the conditions:

* At least `a` people in front ⇒ `pos >= a + 1`
* At most `b` people behind ⇒ `pos >= n - b`

So the earliest valid position is: `max(a + 1, n - b)`

Since the latest possible position is always `n`, the number of valid positions is: `n - max(a + 1, n - b) + 1`

This simplifies to: `min(n - a, b + 1)`

---

### Algorithm

```text id="alg124a"
READ n, a, b

PRINT min(n - a, b + 1)
```

---

## Edge Cases

* `b = 0` → the person must be the last in the line.
* `a = 0` → the person can stand anywhere, subject to the second condition.
* Both constraints are restrictive → the smaller of the two limits determines the answer.
* The formula naturally handles all valid inputs without special cases.

---

## Time and Space Complexity

* **Time Complexity:** `O(1)` - only a few arithmetic operations.
* **Space Complexity:** `O(1)` - no extra space is used.

---

## Java Code

```java id="code124a"
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        int n = Integer.parseInt(st.nextToken());
        int a = Integer.parseInt(st.nextToken());
        int b = Integer.parseInt(st.nextToken());

        System.out.println(Math.min(n - a, b + 1));
    }
}
```
