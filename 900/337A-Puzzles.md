# Codeforces 337A - Puzzles

## Problem

There are `m` puzzle sets, each containing a certain number of pieces.

You must choose exactly `n` puzzle sets such that the difference between the largest and the smallest puzzle in the chosen group is minimized.

Output this minimum possible difference.

---

## Initial Thought Process

* We need to choose exactly `n` puzzle sets.
* A brute-force approach would try every possible combination.
* However, checking all combinations is too expensive.
* We need to find a property that reduces the search space.

---

## Insight

The only values affecting the answer are the **minimum** and **maximum** puzzle sizes in the chosen group.

If the puzzle sizes are sorted, the optimal choice will always be a **contiguous block** of size `n`.

Any non-contiguous selection can only have the same or a larger range than the contiguous block spanning the same values.

---

## Key Observation

After sorting:

* The minimum of a group is the first element.
* The maximum of a group is the last element.
* Every possible group of `n` puzzles becomes a window of size `n`.

So for every valid window:

```
difference = last element - first element
```

Keep the minimum difference across all windows.

---

## Algorithm

```text id="alg337a"
READ n, m

READ puzzle sizes into array

SORT the array

minDiff = infinity

FOR every window of size n
    diff = last element - first element
    minDiff = min(minDiff, diff)

PRINT minDiff
```

---

## Edge Cases

* `n = 1` (answer is always `0`)
* `n = m` (entire array must be chosen)
* Multiple puzzle sets with the same size
* Already sorted input
* Completely unsorted input

---

## Time and Space Complexity

* **Time Complexity:** `O(m log m)` - sorting dominates
* **Space Complexity:** `O(1)` (excluding the sorting implementation)

---

## Java Code

```java id="java337a"
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        StringTokenizer st = new StringTokenizer(br.readLine());
        int n = Integer.parseInt(st.nextToken());
        int m = Integer.parseInt(st.nextToken());

        int[] puzzles = new int[m];

        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < m; i++) {
            puzzles[i] = Integer.parseInt(st.nextToken());
        }

        Arrays.sort(puzzles);

        int minDiff = Integer.MAX_VALUE;

        for (int i = 0; i <= m - n; i++) {
            minDiff = Math.min(minDiff, puzzles[i + n - 1] - puzzles[i]);
        }

        System.out.println(minDiff);
    }
}
```
