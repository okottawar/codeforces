# Question 617A - Elephant

## Problem

An elephant is located at position `0` on a number line and wants to reach position `x`. In one step, the elephant can move forward by `1`, `2`, `3`, `4`, or `5` units. Find the minimum number of steps required to reach position `x`.

---

## Initial Thought Process

* Since the goal is to minimize the number of steps, the elephant should always take the largest possible step.
* A step of length `5` covers the most distance, so we first take as many `5`-unit steps as possible.
* If some distance remains after using all possible `5`-unit steps, one additional step is enough because the remainder will always be between `1` and `4`.

---

## Insight

* The answer is simply the ceiling of `x / 5`.
* Using integer arithmetic:

```text
steps = x / 5

if x % 5 != 0
    steps++
```

* This can also be written as:

```text
steps = (x + 4) / 5
```

which effectively computes `ceil(x / 5)` using integer division.

---

### Algorithm

```text id="alg617a"
READ x

steps = x / 5

IF x % 5 != 0
    steps++

PRINT steps
```

---

## Edge Cases

* `x = 1` → one step of length `1`.
* `x = 5` → exactly one step of length `5`.
* `x = 10` → exactly two steps of length `5`.
* `x = 11` → two steps of length `5` and one additional step.

---

## Time and Space Complexity

* **Time Complexity:** `O(1)` - Only a few arithmetic operations are performed.

* **Space Complexity:** `O(1)` - No extra data structures are used.

---

## Java Code

```java id="code617a"
import java.io.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int x = Integer.parseInt(br.readLine());

        int steps = x / 5;
        if (x % 5 != 0) {
            steps++;
        }

        System.out.println(steps);
    }
}
```
