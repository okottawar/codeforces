# Codeforces 451A - Game With Sticks

## Problem

There is an `n × m` board of sticks.

Two players, **Akshat** and **Malvika**, take turns.

On each move, a player selects an unused intersection, removing one entire row and one entire column from further play.

The player who cannot make a move loses.

Determine the winner if both players play optimally.

---

## Initial Thought Process

* Each move removes one row and one column.
* Initially, it may seem that the answer depends on the total number of cells (`n × m`).
* However, the game is actually governed by how many moves can be made before either all rows or all columns are exhausted.

---

## Insight

Every move consumes:

* One available row
* One available column

Therefore, after each move:

* Remaining rows decrease by `1`
* Remaining columns decrease by `1`

The game ends as soon as either there are no rows left or no columns left.

Hence, the total number of possible moves is exactly:

```
min(n, m)
```

---

## Key Observation

* Akshat plays first.
* Malvika plays second.
* If the total number of moves is odd, Akshat makes the last move.
* If the total number of moves is even, Malvika makes the last move.

Therefore:

* `min(n, m)` is odd → **Akshat wins**
* `min(n, m)` is even → **Malvika wins**

---

## Algorithm

```text id="alg451a"
READ n, m

moves = min(n, m)

IF moves is odd
    PRINT "Akshat"
ELSE
    PRINT "Malvika"
```

---

## Edge Cases

* `n = 1`
* `m = 1`
* `n = m`
* One dimension much larger than the other
* Minimum dimension is already exhausted after one move

---

## Time and Space Complexity

* **Time Complexity:** `O(1)`
* **Space Complexity:** `O(1)`

---

## Java Code

```java id="java451a"
import java.io.*;
import java.util.StringTokenizer;

public class Main {
    public static void main (String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        StringTokenizer st = new StringTokenizer(br.readLine());
        int n = Integer.parseInt(st.nextToken());
        int m = Integer.parseInt(st.nextToken());

        if (Math.min(n, m) % 2 == 1)
            System.out.println("Akshat");
        else
            System.out.println("Malvika");
    }
}
```
