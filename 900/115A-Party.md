# Codeforces 115A - Party

## Problem

Given:

* `n` employees numbered from `1` to `n`.
* For each employee:
  * `-1` means they have no manager (they are a top-level boss).
  * Otherwise, the value is the index of their direct manager.

A party is organized such that:

* Every employee belongs to exactly one group.
* Within a group, each employee's direct manager (if any) must also belong to the same group.

Determine the **minimum number of groups** required.

---

## Initial Thought Process

* Each employee belongs to a management hierarchy.
* The number of groups required depends on the longest chain of managers.
* Therefore, for every employee:
  * Move upward through their managers until reaching a top-level boss.
  * Count the length of that chain.
* The maximum chain length is the answer.

---

## Insight

* The management structure forms a **forest** (multiple trees).
* Every employee has at most one direct manager.
* Starting from any employee and repeatedly moving to their manager eventually reaches a root (`-1`).
* The employee with the deepest management chain determines the minimum number of groups.

---

## Algorithm

```text
READ n

READ manager array

answer = 0

FOR each employee i
    depth = 1
    current = i

    WHILE manager[current] != -1
        depth++
        current = manager[current]

    answer = max(answer, depth)

PRINT answer
```

---

## Edge Cases

* Every employee has `-1` as their manager → answer is `1`.
* A single long management chain → answer equals the number of employees.
* Multiple independent management trees → choose the maximum depth among them.

---

## Time and Space Complexity

* **Time Complexity:** `O(n²)` — in the worst case, each employee traverses a chain of length `n`.
* **Space Complexity:** `O(n)` — stores the manager array.

---

## Java Code

```java
import java.io.*;
import java.util.StringTokenizer;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int n = Integer.parseInt(br.readLine());
        int[] manager = new int[n + 1];
        for (int i = 1; i <= n; i++) {
            manager[i] = Integer.parseInt(br.readLine());
        }

        int answer = 0;
        for (int i = 1; i <= n; i++) {
            int depth = 1;
            int current = i;
            while (manager[current] != -1) {
                depth++;
                current = manager[current];
            }
            answer = Math.max(answer, depth);
        }

        System.out.println(answer);
    }
}
```
