# Codeforces 939A - Love Triangle

## Problem

Given:

* `n` people.
* Every person chooses exactly one other person.
* The choices are given as an array where `a[i]` is the person chosen by person `i`.
* Determine whether there exists a **cycle of exactly length 3** (a love triangle).

Print `"YES"` if such a cycle exists, otherwise print `"NO"`.

---

## Initial Thought Process

* Since the problem is tagged **Graph**, the first instinct is to model the relationships as a directed graph.
* A cycle detection algorithm like DFS seems applicable.
* However, the problem is **not asking whether any cycle exists**—it specifically asks for a cycle of length `3`.

---

## Insight

* Every person has **exactly one outgoing edge**.
* This means there is only one possible path starting from any person.
* Instead of building a graph, the input array itself represents the graph.
* For every person `i`, simply follow three consecutive choices:
  * `a = next[i]`
  * `b = next[a]`
  * `c = next[b]`
* If `c == i`, then

```
i → a → b → i
```

forms a cycle of exactly length `3`.

No DFS or graph traversal is required.

---

## Algorithm

```text id="alg939a"
READ n

READ array next[]
CONVERT values to 0-based indexing

FOR every person i
    a = next[i]
    b = next[a]
    c = next[b]

    IF c == i
        PRINT "YES"
        EXIT

PRINT "NO"
```

---

## Edge Cases

* No cycles exist → print `"NO"`.
* A cycle longer than `3` exists → print `"NO"`.
* Multiple disconnected components → every starting node is checked independently.
* More than one 3-cycle exists → the first detected one immediately returns `"YES"`.

---

## Time and Space Complexity

* **Time Complexity:** `O(n)` — each person is checked once using only three array accesses.
* **Space Complexity:** `O(n)` — the input array is stored.

---

## Java Code

```java id="code939a"
import java.io.*;
import java.util.StringTokenizer;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        int n = Integer.parseInt(br.readLine());
        StringTokenizer st = new StringTokenizer(br.readLine());

        int[] next = new int[n];

        for (int i = 0; i < n; i++) {
            next[i] = Integer.parseInt(st.nextToken()) - 1;
        }

        for (int i = 0; i < n; i++) {
            int a = next[i];
            int b = next[a];
            int c = next[b];

            if (c == i) {
                System.out.println("YES");
                return;
            }
        }

        System.out.println("NO");
    }
}
```
