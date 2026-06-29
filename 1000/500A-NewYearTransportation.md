# Question 500A - New Year Transportation

## Problem

You are given a transportation system with `n` cells.

From cell `i`, you can move exactly `ai` cells forward.

Starting from cell `1`, determine whether it is possible to reach cell `t`.

Print:

* `"YES"` if cell `t` can be reached.
* `"NO"` otherwise.

---

## Initial Thought Process

* Each cell has exactly one possible next move.

* We need to simulate the journey starting from cell `1`.

* At every step:

  * Move from the current position by the jump value stored at that position.
  * Continue until:

    * We reach `t`.
    * We go beyond `t`.

---

## Insight

* The array represents **directed jumps**, not values to add together.
* The next position is: `next position = current position + jump[current position]`
* Since we only move forward, we can never visit a previous cell.
* Therefore, simple simulation is enough.

---

### Algorithm

```text id="alg500a"
READ n and target t

STORE jump values

SET position = 1

WHILE position < t:
    position += jump[position]

IF position == t:
    PRINT YES
ELSE:
    PRINT NO
```

---

## Edge Cases

* Target is the first cell: `n = 1, t = 1`


Already at the destination.

* Jump skips over the target: position becomes greater than t

Answer is `"NO"`.

* Direct jump to target: `1 -> t`

Answer is `"YES"`.

* Chain of multiple jumps required.

---

## Time and Space Complexity

* **Time Complexity:** `O(n)` - each cell is visited at most once.
* **Space Complexity:** `O(n)` - jump values are stored.

---

## Java Code

```java id="code500a"
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        int n = Integer.parseInt(st.nextToken());
        int t = Integer.parseInt(st.nextToken());

        int[] jump = new int[n + 1];
        st = new StringTokenizer(br.readLine());
        for (int i = 1; i < n; i++) {
            jump[i] = Integer.parseInt(st.nextToken());
        }

        int pos = 1;
        while (pos < t) {
            pos += jump[pos];
        }

        if (pos == t) {
            System.out.println("YES");
        } else {
            System.out.println("NO");
        }
    }
}
```
