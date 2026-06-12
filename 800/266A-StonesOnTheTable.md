# Question 266A - Stones on the Table

## Problem

You are given a row of `n` stones, each colored either Red (`R`), Green (`G`), or Blue (`B`).

You need to remove the minimum number of stones so that no two adjacent stones have the same color.

---

## Initial Thought Process

* The key requirement is that no two consecutive stones should be identical.
* If two adjacent stones have the same color, one of them must be removed.
* Instead of simulating removals, we can directly count such problematic pairs.

---

## Insight

* Every time `stones[i] == stones[i+1]`, one removal is required.
* Counting these adjacent equal pairs gives the minimum number of removals.
* No need for complex data structures or greedy simulation.

---

### Algorithm

```text id="alg266a"
READ integer n
READ string stones

count = 0

FOR i from 0 to n - 2:
    IF stones[i] == stones[i + 1]:
        count++

PRINT count
```

---

## Edge Cases

* All stones are different → output is `0`
* All stones are same → output is `n - 1`
* Alternating colors (e.g., `RGRGRG`) → output is `0`
* Single stone → output is `0`

---

## Time and Space Complexity

* **Time Complexity:** `O(n)` - One pass through the string.

* **Space Complexity:** `O(1)` - Only a counter is used.

---

## Java Code

```java id="code266a"
import java.io.*;

public class Main {
    public static void main (String [] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        int n = Integer.parseInt(br.readLine());
        String stones = br.readLine();

        int count = 0;

        for (int i = 0; i < n - 1; i++) {
            if (stones.charAt(i) == stones.charAt(i + 1)) {
                count++;
            }
        }

        System.out.println(count);
    }
}
```
