# Question 231A - Team

## Problem

Given n problems and the opinions of 3 students for each problem (0 or 1), determine how many problems will be implemented.

A problem is implemented if **at least 2 out of 3 students agree** (i.e., the sum of opinions ≥ 2).

---

## Initial Thought Process

* Read input for each problem (3 values per line)
* Convert each line into three integers
* Compute sum of the three values
* If sum ≥ 2, increment the counter

---

## Insight

* Each problem is decided by majority voting among 3 students
* Instead of checking multiple conditions, the problem can be reduced to a simple sum check
* Condition simplifies to:

  * `a + b + c ≥ 2 → problem is accepted`
* This avoids complex logical expressions or bitwise operations

---

## Algorithm

```
INPUT n
SET count = 0

FOR i = 1 TO n
    READ a, b, c

    IF (a + b + c) >= 2
        count = count + 1

PRINT count
```

---

## Edge Cases

* n = 1 → only one decision is made
* All inputs are 0 0 0 → output = 0
* All inputs are 1 1 1 → output = n
* Mixed cases with exactly two 1s per row → all counted

---

## Time and Space Complexity

* **Time Complexity:** `O(n)` where n is number of problems
* **Space Complexity:** `O(1)` (only storing counters and variables)

---

## Java Code

```java
import java.io.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        int n = Integer.parseInt(br.readLine());
        int count = 0;

        for (int i = 0; i < n; i++) {
            String[] parts = br.readLine().split(" ");

            int a = Integer.parseInt(parts[0]);
            int b = Integer.parseInt(parts[1]);
            int c = Integer.parseInt(parts[2]);

            if (a + b + c >= 2) {
                count++;
            }
        }

        System.out.println(count);
    }
}
```
