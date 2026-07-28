# Codeforces 1055A - Metro

## Problem

Given:

* `n` stations numbered from `1` to `n`.
* Bob starts at station `1`.
* Alice's home is at station `s`.
* `a[i]` indicates whether the train on the first track stops at station `i`.
* `b[i]` indicates whether the train on the second track stops at station `i`.

Rules:

* The first track moves only from left to right.
* The second track moves only from right to left.
* You may switch tracks only at stations where both trains stop.

Determine whether Bob can reach station `s`.

---

## Initial Thought Process

* Bob starts on the first track at station `1`.
* If the first track reaches station `s`, the answer is immediately **YES**.
* Otherwise, Bob must:
  * travel past `s` on the first track,
  * switch to the second track at some station,
  * travel back to station `s`.
* Therefore, the only thing to check is whether such a switching station exists.

---

## Insight

* If `a[1] == 0`, Bob cannot even leave the starting station.
* If `a[s] == 1`, Bob can directly reach station `s` using the first track.
* Otherwise:
  * `b[s]` must be `1`, otherwise the second track never stops at `s`.
  * There must exist some station `i ≥ s` such that:
    * `a[i] == 1`
    * `b[i] == 1`
* Such a station allows Bob to move right on the first track, switch tracks, and travel left back to station `s`.

---

## Algorithm

```text
READ n, s

READ arrays a and b

IF a[1] == 0
    PRINT "NO"

ELSE IF a[s] == 1
    PRINT "YES"

ELSE IF b[s] == 0
    PRINT "NO"

FOR i = s TO n
    IF a[i] == 1 AND b[i] == 1
        PRINT "YES"

PRINT "NO"
```

---

## Edge Cases

* `a[1] == 0` → Bob cannot start the journey.
* `a[s] == 1` → destination is directly reachable.
* `b[s] == 0` → impossible to return to station `s` using the second track.
* No station at or after `s` allows switching → destination cannot be reached.

---

## Time and Space Complexity

* **Time Complexity:** `O(n)` — a single scan of the arrays.
* **Space Complexity:** `O(n)` — stores the two track arrays.

---

## Java Code

```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        StringTokenizer st = new StringTokenizer(br.readLine());
        int n = Integer.parseInt(st.nextToken());
        int s = Integer.parseInt(st.nextToken());

        int[] a = new int[n + 1];
        int[] b = new int[n + 1];

        st = new StringTokenizer(br.readLine());
        for (int i = 1; i <= n; i++) {
            a[i] = Integer.parseInt(st.nextToken());
        }

        st = new StringTokenizer(br.readLine());
        for (int i = 1; i <= n; i++) {
            b[i] = Integer.parseInt(st.nextToken());
        }

        if (a[1] == 0) {
            System.out.println("NO");
            return;
        }

        if (a[s] == 1) {
            System.out.println("YES");
            return;
        }

        if (b[s] == 0) {
            System.out.println("NO");
            return;
        }

        for (int i = s; i <= n; i++) {
            if (a[i] == 1 && b[i] == 1) {
                System.out.println("YES");
                return;
            }
        }

        System.out.println("NO");
    }
}
```
