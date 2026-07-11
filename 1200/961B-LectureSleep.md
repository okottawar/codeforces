# Question B - Lecture Sleep

## Problem

Given:

* `a[i]` = number of theorems taught during the `i-th` minute.
* `t[i]` = `1` if Mishka is awake, `0` if asleep.

Mishka automatically writes down theorems during awake minutes.

You can use a secret technique **exactly once** to keep him awake for **`k` consecutive minutes**.

Find the maximum number of theorems Mishka can write down.

---

## Initial Thought Process

* Count all theorems Mishka already writes while awake.
* The only benefit of using the technique is during minutes when he is asleep.
* Find the `k`-length window that contains the maximum number of missed theorems.

---

## Insight

* The answer consists of two parts:

  * **Base theorems** already written (`t[i] == 1`).
  * **Extra theorems** gained by waking Mishka during one window.
* While checking each window, only add values where `t[i] == 0`.
* A sliding window efficiently finds the maximum extra theorems in `O(n)` time.

---

## Algorithm

```text id="alg961b"
READ n, k

READ array a
READ array t

base = 0

FOR each minute
    IF t[i] == 1
        base += a[i]

extra = sum of a[i] where t[i] == 0 in first k minutes
maxExtra = extra

FOR each remaining window
    ADD entering sleeping minute (if any)
    REMOVE leaving sleeping minute (if any)
    UPDATE maxExtra

PRINT base + maxExtra
```

---

## Edge Cases

* `k = n` → Mishka is awake for the entire lecture.
* Mishka is already awake throughout → answer is simply the sum of all theorems.
* Mishka sleeps throughout → answer is the maximum sum of any `k` consecutive minutes.
* `k = 1` → choose the single sleeping minute with the most theorems.

---

## Time and Space Complexity

* **Time Complexity:** `O(n)` — one pass for base sum and one sliding window pass.
* **Space Complexity:** `O(n)` — stores the two input arrays.

---

## Java Code

```java id="code961b"
import java.io.*;
import java.util.StringTokenizer;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        int n = Integer.parseInt(st.nextToken());
        int k = Integer.parseInt(st.nextToken());

        int[] a = new int[n];
        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < n; i++) {
            a[i] = Integer.parseInt(st.nextToken());
        }

        int[] t = new int[n];
        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < n; i++) {
            t[i] = Integer.parseInt(st.nextToken());
        }

        int base = 0;
        for (int i = 0; i < n; i++) {
            if (t[i] == 1) {
                base += a[i];
            }
        }

        int extra = 0;
        for (int i = 0; i < k; i++) {
            if (t[i] == 0) {
                extra += a[i];
            }
        }

        int maxExtra = extra;
        for (int i = k; i < n; i++) {
            if (t[i] == 0) extra += a[i];
            if (t[i - k] == 0) extra -= a[i - k];
            maxExtra = Math.max(maxExtra, extra);
        }

        System.out.println(base + maxExtra);
    }
}
```
