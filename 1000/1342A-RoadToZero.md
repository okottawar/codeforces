# Question 1342A - Road To Zero

## Problem

Given two integers `x` and `y`.

Operations:

* Decrease either `x` or `y` by `1` → cost `a`
* Decrease both `x` and `y` by `1` → cost `b`

Find the minimum cost to make both values `0`.

---

## Initial Thought Process

* Reduce both numbers together while possible.
* Once one becomes `0`, reduce the remaining value individually.
* However, using the second operation is not always cheaper.

---

## Insight

To decrease both numbers by `1`:

* One joint operation costs `b`
* Two individual operations cost `2 * a`

So for every common reduction, use:

```text id="effective-cost"
min(b, 2 * a)
```

Let:

```text id="common"
m = min(x, y)
```

Then:

* Reduce both numbers `m` times.
* Reduce the remaining difference individually.

---

### Algorithm

```text id="alg1342a"
m = min(x, y)

cost = m * min(b, 2 * a)

cost += abs(x - y) * a

PRINT cost
```

---

## Time and Space Complexity

* **Time Complexity:** `O(1)`
* **Space Complexity:** `O(1)`

---

## Java Code

```java id="code1342a"
import java.io.*;
import java.util.StringTokenizer;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(
                new InputStreamReader(System.in));

        int t = Integer.parseInt(br.readLine());

        while (t-- > 0) {
            StringTokenizer st = new StringTokenizer(br.readLine());

            long x = Long.parseLong(st.nextToken());
            long y = Long.parseLong(st.nextToken());

            st = new StringTokenizer(br.readLine());

            long a = Long.parseLong(st.nextToken());
            long b = Long.parseLong(st.nextToken());

            long m = Math.min(x, y);

            long cost = m * Math.min(b, 2L * a)
                      + Math.abs(x - y) * a;

            System.out.println(cost);
        }
    }
}
```
