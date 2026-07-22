# Codeforces 492B - Vanya and Lanterns

## Problem

Given:

* `n` lanterns placed along a street.
* `l` = length of the street.
* `lights[i]` = position of the `i-th` lantern.

Every lantern illuminates the same distance `d` to its left and right.

Find the **minimum** value of `d` such that the **entire street** from `0` to `l` is illuminated.

---

## Initial Thought Process

* The lanterns affect only the intervals around their positions.
* The largest uncovered gap determines the minimum required radius.
* Since the lantern positions are unordered, sort them first.
* Also remember to check the street's two ends, since they are covered by only one lantern each.

---

## Insight

* After sorting the lantern positions:

  * The left end requires a radius of at least `lights[0]`.
  * The right end requires a radius of at least `l - lights[n - 1]`.
  * Between two consecutive lanterns, each lantern covers half of the gap.
* Therefore, the answer is the maximum among:

  * Distance from the left end to the first lantern.
  * Distance from the last lantern to the right end.
  * Half of the largest gap between consecutive lanterns.

---

## Algorithm

```text id="alg492b"
READ n, l

READ array lights

SORT lights

answer = max(
    lights[0],
    l - lights[n - 1]
)

FOR every adjacent pair
    gap = lights[i + 1] - lights[i]
    answer = max(answer, gap / 2)

PRINT answer
```

---

## Edge Cases

* Only one lantern → it must illuminate both ends of the street.
* A lantern is placed at `0` or `l` → one endpoint already has full coverage.
* Largest gap occurs between two lanterns → required radius is half of that gap.
* Largest uncovered distance is at one of the street ends instead of between lanterns.

---

## Time and Space Complexity

* **Time Complexity:** `O(n log n)` — sorting the lantern positions dominates the runtime.
* **Space Complexity:** `O(n)` — stores the lantern positions.

---

## Java Code

```java id="code492b"
import java.io.*;
import java.util.*;

public class Main {
    public static void main (String [] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        int n = Integer.parseInt(st.nextToken());
        long l = Long.parseLong(st.nextToken());

        long[] lights = new long[n];

        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < n; i++) {
            lights[i] = Long.parseLong(st.nextToken());
        }

        Arrays.sort(lights);

        double ans = Math.max(lights[0], l - lights[n - 1]);

        for (int i = 0; i < n - 1; i++) {
            ans = Math.max(ans, (lights[i + 1] - lights[i]) / 2.0);
        }

        System.out.printf("%.10f\n", ans);
    }
}
```
