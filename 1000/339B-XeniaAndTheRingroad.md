# Question 339B - Xenia and Ringroad

## Problem

There are `n` houses arranged in a circle, numbered from `1` to `n` in order. After house `n`, the numbering wraps back to `1`.

Xenia starts at house `1` and has to complete `m` tasks. Each task specifies a house she must visit, in a fixed order.

She moves step by step along the ring, always moving in the increasing direction (clockwise). Moving from house `i` to `i+1` takes 1 step, and moving from `n` goes back to `1` also takes 1 step.

The goal is to find the total number of steps required to complete all tasks in order.

---

## Initial Thought Process

* Movement is circular.
* At each step, we move from current house to next required house.
* We need to accumulate total distance.

---

## Insight

* We do NOT jump directly; we move step-by-step along the circle.
* We always move in one direction (clockwise).
* If the target house is behind the current position, we complete a full cycle wrap-around.

---

## Key Idea

Compute distance between consecutive positions:

### If forward move is possible:

```text id="case1"
curr ≤ target
distance = target - curr
```

### If wrap-around is needed:

```text id="case2"
curr > target
distance = (n - curr) + target
```

---

## Algorithm

```text id="alg339b"
curr = 1
steps = 0

FOR each target in list:
    IF target >= curr:
        steps += target - curr
    ELSE:
        steps += (n - curr) + target

    curr = target

PRINT steps
```

---

## Edge Cases

* First move always starts from house `1`
* Repeated same house → 0 steps
* No backward movement allowed (only circular forward motion)
* Use `long` for total steps (can be large)

---

## Time and Space Complexity

* **Time Complexity:** `O(m)`
* **Space Complexity:** `O(1)` extra (excluding input)

---

## Java Code

```java id="code339b"
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        StringTokenizer st = new StringTokenizer(br.readLine());
        int n = Integer.parseInt(st.nextToken());
        int m = Integer.parseInt(st.nextToken());

        st = new StringTokenizer(br.readLine());

        long steps = 0;
        int curr = 1;

        for (int i = 0; i < m; i++) {
            int target = Integer.parseInt(st.nextToken());

            if (target >= curr) {
                steps += target - curr;
            } else {
                steps += (n - curr) + target;
            }

            curr = target;
        }

        System.out.println(steps);
    }
}
```
