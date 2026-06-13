# Question 1A - Theatre Square

## Problem

Given a rectangle of size `n × m`, we must cover it completely using square tiles of size `a × a`.
Tiles cannot be broken, and they may extend beyond the rectangle boundaries.
Find the minimum number of tiles required.

---

## Initial Thought Process

* Treat the problem as covering each dimension independently.
* First determine how many tiles are needed along the length `n`.
* Then determine how many tiles are needed along the width `m`.
* Multiply both results to get total tiles.

---

## Insight

* A single tile covers `a` units.
* If a dimension is not perfectly divisible by `a`, we still need an extra tile.
* So for each dimension:

  * If divisible → `n / a`
  * Otherwise → `n / a + 1`
* This avoids using floating-point math and keeps logic simple.

---

### Algorithm

```text id="alg1a"
READ n, m, a

IF n % a == 0:
    tilesAlongN = n / a
ELSE:
    tilesAlongN = n / a + 1

IF m % a == 0:
    tilesAlongM = m / a
ELSE:
    tilesAlongM = m / a + 1

answer = tilesAlongN * tilesAlongM

PRINT answer
```

---

## Edge Cases

* `n < a` → requires 1 tile along that dimension.
* `m < a` → requires 1 tile along that dimension.
* Exactly divisible values → no extra tile needed.
* Very large inputs → require `long` to avoid overflow.

---

## Time and Space Complexity

* **Time Complexity:** `O(1)` - constant arithmetic operations.
* **Space Complexity:** `O(1)` - only a few variables used.

---

## Java Code (Your Solution)

```java id="code1a"
import java.io.*;
import java.util.StringTokenizer;

public class Main {

    public static void main (String [] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        long n = Long.parseLong(st.nextToken());
        long m = Long.parseLong(st.nextToken());
        long a = Long.parseLong(st.nextToken());

        long tilesAlongN;
        long tilesAlongM;

        if (n % a == 0) {
            tilesAlongN = n / a;
        } else {
            tilesAlongN = n / a + 1;
        }

        if (m % a == 0) {
            tilesAlongM = m / a;
        } else {
            tilesAlongM = m / a + 1;
        }

        System.out.println(tilesAlongN * tilesAlongM);
    }
}
```
