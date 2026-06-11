# Question 50A - Domino Piling

## Problem

Given an `M × N` board and dominoes of size `2 × 1`, find the maximum number of dominoes that can be placed without overlap.

---

## Initial Thought Process

* Each domino covers 2 cells.
* Find the total number of cells in the board.
* Divide by 2 to get the maximum number of dominoes.

---

## Insight

* Board area = `M × N`
* Domino area = `2`
* Answer = `[(M × N) / 2]`

---

## Algorithm

```
INPUT m, n

PRINT (m * n) / 2
```

---

## Edge Cases

* Odd board area → one cell remains uncovered
* `1 × 1` board → answer = 0

---

## Time and Space Complexity

* **Time Complexity:** `O(1)`
* **Space Complexity:** `O(1)`

---

## Java Code

```java
import java.io.*;
import java.util.StringTokenizer;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        int m = Integer.parseInt(st.nextToken());
        int n = Integer.parseInt(st.nextToken());

        System.out.println((m * n) / 2);
    }
}
```
