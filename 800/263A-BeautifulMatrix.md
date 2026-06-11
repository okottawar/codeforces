# Question 263A - Beautiful Matrix

## Problem

Given a `5 × 5` matrix containing exactly one `1`, find the minimum number of moves required to bring the `1` to the center of the matrix.

---

## Initial Thought Process

* Locate the position of `1`.
* Determine how far it is from the center.
* Each move changes the row or column by 1.

---

## Insight

* The center of a `5 × 5` matrix is `(2, 2)`.
* The minimum number of moves is the Manhattan distance from the position of `1` to the center.

```text
moves = |row - 2| + |col - 2|
```

---

## Algorithm

```text
FOR each cell in the matrix
    IF value == 1
        store its row and column

PRINT |row - 2| + |col - 2|
```

---

## Edge Cases

* `1` is already at the center → answer = 0
* `1` is in a corner → maximum distance

---

## Time and Space Complexity

* **Time Complexity:** `O(25)` ≈ `O(1)`
* **Space Complexity:** `O(1)`

---

## Java Code

```java
import java.io.*;
import java.util.StringTokenizer;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        int row = 0;
        int col = 0;

        for (int i = 0; i < 5; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());

            for (int j = 0; j < 5; j++) {
                int x = Integer.parseInt(st.nextToken());

                if (x == 1) {
                    row = i;
                    col = j;
                }
            }
        }

        System.out.println(Math.abs(row - 2) + Math.abs(col - 2));
    }
}
```
