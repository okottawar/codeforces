# Question 69A - Young Physicist

## Problem

You are given `n` force vectors in 3D space.
Each vector has components `(x, y, z)`.

The system is in equilibrium if the **sum of all vectors equals zero**, meaning:

* Sum of all x-components = 0
* Sum of all y-components = 0
* Sum of all z-components = 0

Determine whether the system is in equilibrium.

---

## Initial Thought Process

* Each line contains a 3D vector `(x, y, z)`.
* We need to track total movement in each axis separately.
* At the end, check whether all three totals are zero.

---

## Insight

* The problem is about **vector cancellation**.
* Each dimension is independent, so they must be tracked separately.

---

### Algorithm

```text id="alg69a"
READ n

INITIALIZE xSum = 0, ySum = 0, zSum = 0

FOR i from 1 to n:
    READ x, y, z
    xSum += x
    ySum += y
    zSum += z

IF xSum == 0 AND ySum == 0 AND zSum == 0:
    PRINT "YES"
ELSE:
    PRINT "NO"
```

---

## Edge Cases

* `n = 1` → only valid if vector is `(0,0,0)`
* All vectors cancel out pairwise → valid equilibrium
* Any imbalance in even one axis → not in equilibrium

---

## Time and Space Complexity

* **Time Complexity:** `O(n)` - one pass through all vectors
* **Space Complexity:** `O(1)` - only three variables used

---

## Java Code

```java id="code69a"
import java.io.*;
import java.util.StringTokenizer;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        int n = Integer.parseInt(br.readLine());

        int xSum = 0, ySum = 0, zSum = 0;

        for (int i = 0; i < n; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());

            xSum += Integer.parseInt(st.nextToken());
            ySum += Integer.parseInt(st.nextToken());
            zSum += Integer.parseInt(st.nextToken());
        }

        System.out.println((xSum == 0 && ySum == 0 && zSum == 0) ? "YES" : "NO");
    }
}
```
