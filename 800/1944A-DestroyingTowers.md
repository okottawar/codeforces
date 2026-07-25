# Codeforces 1944A - Destroying Bridges

## Problem

Given:

* `n` islands connected as a **complete graph**.
* Every pair of islands is connected by exactly one bridge.
* Exactly `k` bridges are destroyed **optimally** to minimize the number of islands reachable from island `1`.

Find the **minimum number of islands** that can still be reached from island `1`.

---

## Initial Thought Process

* A complete graph initially has

  ```
  n × (n - 1) / 2
  ```

  bridges.

* The first instinct is to count how many bridges remain after destruction.
* However, the **number of remaining bridges does not determine connectivity**.
* In a complete graph, many bridges can be destroyed while the graph still remains connected.

---

## Insight

* To make an island unreachable from island `1`, **every bridge connecting that island to the rest of the graph must be destroyed**.
* Each island has exactly `n - 1` incident bridges.
* Therefore:
  * If `k < n - 1`, it is impossible to isolate any island.
    * All `n` islands remain reachable.
  * If `k >= n - 1`, at least one island (including possibly island `1` itself) can be isolated.
    * The minimum reachable islands become `1`.

The answer depends only on whether `k` is less than `n - 1`.

---

## Algorithm

```text
READ t

FOR each test case
    READ n, k

    IF k < n - 1
        PRINT n
    ELSE
        PRINT 1
```

---

## Edge Cases

* `k = 0` → no bridges are destroyed, so all islands remain reachable.
* `k < n - 1` → the graph cannot be disconnected.
* `k = n - 1` → exactly enough bridges exist to isolate one island.
* `k` is very large → regardless of how many additional bridges are removed, the minimum reachable islands remain `1`.

---

## Time and Space Complexity

* **Time Complexity:** `O(1)` per test case.
* **Space Complexity:** `O(1)`.

---

## Java Code

```java
import java.io.*;
import java.util.StringTokenizer;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        int t = Integer.parseInt(br.readLine());

        while (t-- > 0) {
            StringTokenizer st = new StringTokenizer(br.readLine());

            int n = Integer.parseInt(st.nextToken());
            int k = Integer.parseInt(st.nextToken());

            if (k < n - 1)
                System.out.println(n);
            else
                System.out.println(1);
        }
    }
}
```
