# Codeforces 450A - Jzzhu and Children

## Problem

There are `n` children in a queue. Each child `i` has `a[i]` candies.

Each time, the first child in the queue receives `m` candies and goes to the end of the queue. If after receiving candies, a child has `0` or fewer candies remaining, they leave the queue.

You need to determine the **index of the last child to leave the queue**.

---

## Initial Thought Process

* The process is repetitive and cyclic.
* Each child keeps receiving `m` candies per turn.
* A child leaves when their total demand is satisfied.
* The problem is equivalent to finding who survives the longest in this cycle.

---

## Insight

Each child effectively needs a certain number of visits to the front of the queue before leaving.

For a child with `a[i]` candies: `number of visits needed = ceil(a[i] / m)`

This is because each visit removes `m` candies.

We can compute this as: `rounds = (a[i] + m - 1) / m`

---

### Key Observation

The last child to leave is:

* The child with the **maximum number of required visits**
* If multiple children have the same value, the **child with the largest index** leaves last (because they appear later in the queue cycle and survive equally long)

---

## Algorithm

```text id="algo450a"
maxRounds = -1
answer = -1

FOR i from 0 to n-1:

    rounds = (a[i] + m - 1) / m

    IF rounds >= maxRounds:
        maxRounds = rounds
        answer = i + 1   // 1-based index

PRINT answer
```

---

## Edge Cases

* All children have equal `a[i]`
* `a[i] ≤ m` (some leave in one visit)
* Only one child (`n = 1`)
* Large values of `a[i]`

---

## Time and Space Complexity

* **Time Complexity:** `O(n)`
* **Space Complexity:** `O(1)`

---

## Java Code

```java id="code450a"
import java.io.*;
import java.util.StringTokenizer;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        StringTokenizer st = new StringTokenizer(br.readLine());

        int n = Integer.parseInt(st.nextToken());
        int m = Integer.parseInt(st.nextToken());

        st = new StringTokenizer(br.readLine());

        int maxRounds = -1;
        int answer = -1;

        for (int i = 0; i < n; i++) {
            int a = Integer.parseInt(st.nextToken());

            int rounds = (a + m - 1) / m;

            if (rounds >= maxRounds) {
                maxRounds = rounds;
                answer = i + 1;
            }
        }

        System.out.println(answer);
    }
}
```
