# Question 476A - Dreamoon and Stairs

## Problem

Dreamoon wants to climb exactly `n` stairs.

He can move:

* `1` stair at a time
* `2` stairs at a time

The total number of moves must be divisible by `m`. Find the **minimum possible number of moves** needed to reach exactly the `n`-th stair such that the number of moves is divisible by `m`.

If it is impossible, print `-1`.

---

## Initial Thought Process

* To minimize the number of moves, we should use as many `2-step` moves as possible.
* However, the total number of moves must also be divisible by `m`.
* Therefore:

  * First determine the **minimum number of moves** that can reach `n`.
  * Then find the smallest multiple of `m` that is at least that minimum.
  * Verify that this number of moves does not exceed `n`.

---

## Insight

For a fixed number of stairs `n`:

* Maximum moves = `n` (all 1-step moves)
* Minimum moves = `ceil(n / 2)`
* Every move can cover at most 2 stairs.
* Therefore we need at least `ceil(n/2)` moves.

Any move count between:
```text
ceil(n/2) ... n
```
is achievable by replacing some 2-step moves with 1-step moves.

So the task becomes:
> Find the smallest multiple of `m` that lies within the range `[ceil(n/2), n]`.

---

## Algorithm

```text id="alg476a"
minMoves = ceil(n / 2)

ans = smallest multiple of m >= minMoves

IF ans > n:
    PRINT -1
ELSE:
    PRINT ans
```

Using integer arithmetic:

```text
minMoves = (n + 1) / 2

ans = ((minMoves + m - 1) / m) * m
```

---

## Edge Cases

* `n = 1, m = 1` → answer is `1`
* `n = 2, m = 2` → answer is `2`
* `n = 3, m = 2` → answer is `2`
* No multiple of `m` exists in `[ceil(n/2), n]` → `-1`
* `m > n` often leads to `-1`

---

## Time and Space Complexity

* **Time Complexity:** `O(1)`
* **Space Complexity:** `O(1)`

---

## Java Code

```java id="code476a"
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        int n = Integer.parseInt(st.nextToken());
        int m = Integer.parseInt(st.nextToken());

        int minMoves = (n + 1) / 2;

        int ans = ((minMoves + m - 1) / m) * m;

        System.out.println(ans > n ? -1 : ans);
    }
}
```
