# Codeforces 948A - Protect Sheep

## Problem

Given a farm represented as a grid:

* `'S'` = Sheep
* `'W'` = Wolf
* `'.'` = Empty cell

You may place dogs (`'D'`) in any empty cells.

Determine whether it is possible to protect every sheep so that no wolf is directly adjacent (up, down, left, or right) to a sheep.

If possible, print `"Yes"` and the modified grid. Otherwise, print `"No"`.

---

## Initial Thought Process

* A sheep is only in danger if a wolf is already adjacent to it.
* If that happens, placing a dog cannot separate them because they already occupy neighboring cells.
* Otherwise, placing dogs in all empty cells blocks every possible path a wolf could take.

---

## Insight

* Check every wolf in the grid.
* If any neighboring cell contains a sheep, the answer is immediately `"No"`.
* If no such pair exists, simply replace every `'.'` with `'D'`.
* This guarantees that wolves cannot move into empty cells to reach any sheep.

---

## Algorithm

```text id="alg948a"
READ r, c

READ the grid

FOR every cell
    IF cell contains 'W'
        CHECK its 4 neighbors
        IF any neighbor is 'S'
            PRINT "No"
            EXIT

FOR every cell
    IF cell is '.'
        REPLACE it with 'D'

PRINT "Yes"
PRINT the modified grid
```

---

## Edge Cases

* A wolf is already adjacent to a sheep → impossible, print `"No"`.
* No wolves in the grid → replace all empty cells with dogs.
* No sheep in the grid → always possible.
* No empty cells → simply verify that no wolf is adjacent to a sheep.

---

## Time and Space Complexity

* **Time Complexity:** `O(r × c)` — every cell is visited once, and each wolf checks at most four neighbors.
* **Space Complexity:** `O(r × c)` — stores the input grid.

---

## Java Code

```java id="code948a"
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        int r = Integer.parseInt(st.nextToken());
        int c = Integer.parseInt(st.nextToken());

        char[][] grid = new char[r][c];

        for (int i = 0; i < r; i++) {
            grid[i] = br.readLine().toCharArray();
        }

        int[] dr = {-1, 1, 0, 0};
        int[] dc = {0, 0, -1, 1};

        for (int i = 0; i < r; i++) {
            for (int j = 0; j < c; j++) {
                if (grid[i][j] == 'W') {
                    for (int k = 0; k < 4; k++) {
                        int nr = i + dr[k];
                        int nc = j + dc[k];

                        if (nr >= 0 && nr < r && nc >= 0 && nc < c &&
                                grid[nr][nc] == 'S') {
                            System.out.println("No");
                            return;
                        }
                    }
                }
            }
        }

        StringBuilder sb = new StringBuilder();
        sb.append("Yes\n");

        for (int i = 0; i < r; i++) {
            for (int j = 0; j < c; j++) {
                if (grid[i][j] == '.') {
                    grid[i][j] = 'D';
                }
            }
            sb.append(grid[i]).append('\n');
        }

        System.out.print(sb);
    }
}
```
