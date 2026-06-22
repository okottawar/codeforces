# Question 405A - Gravity Flip

## Problem

Given the heights of `n` columns of cubes, gravity is flipped to the right.

After all cubes slide as far right as possible, print the final heights of the columns.

---

## Initial Thought Process

* Simulating the movement of every cube would be complicated.
* Instead, observe what the final arrangement looks like after gravity settles.
* The relative positions of cubes change until shorter columns appear before taller columns.

---

## Insight

* After gravity is flipped, cubes slide right until there are no gaps.
* The final arrangement is simply the column heights in sorted order.

---

## Algorithm

```text
READ n
READ array heights

SORT heights

PRINT heights
```

---

## Edge Cases

* Only one column → remains unchanged
* All columns have the same height → remains unchanged
* Heights already sorted → no change after sorting
* Heights in reverse order → become increasing after sorting

---

## Time and Space Complexity

* **Time Complexity:** `O(n log n)`
* **Space Complexity:** `O(1)` 

---

## Java Code

```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int n = Integer.parseInt(br.readLine());
        int[] arr = new int[n];
        StringTokenizer st = new StringTokenizer(br.readLine());
        for (int i = 0; i < n; i++) {
            arr[i] = Integer.parseInt(st.nextToken());
        }

        Arrays.sort(arr);

        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < n; i++) {
            if (i > 0) {
                sb.append(" ");
            }
            sb.append(arr[i]);
        }

        System.out.println(sb);
    }
}
```
