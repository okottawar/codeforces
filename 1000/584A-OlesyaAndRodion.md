# Question 584A - Olesya and Rodion

## Problem

Given two integers `n` and `t`:

* Find any **n-digit number** that is divisible by `t`.
* If no such n-digit number exists, print `-1`.

Constraints:

* `1 ≤ n ≤ 9`
* `1 ≤ t ≤ 10`

---

## Initial Thought Process

* An n-digit number ranges from `10^(n-1)` to `10^n - 1`
* One approach is to start from the smallest n-digit number and search for a multiple of `t`
* However, brute force is unnecessary because the constraints allow direct construction

---

## Insight

### Case 1: `t` is from 1 to 9

We can construct:

```
t × 10^(n-1)
```

This produces a number:

```
t000...000
```

(with `n-1` zeros)

Properties:

* Has exactly `n` digits
* Is divisible by `t`

Examples:

* `n = 3, t = 2 → 200`
* `n = 4, t = 7 → 7000`

### Case 2: `t = 10`

A number divisible by 10 must end with `0`.

* If `n = 1`, no 1-digit multiple of 10 exists → print `-1`
* Otherwise, print:

```
1000...000
```

(1 followed by `n-1` zeros)

Examples:

* `n = 2 → 10`
* `n = 3 → 100`

---

## Algorithm

```
INPUT n, t

IF t == 10
    IF n == 1
        PRINT -1
    ELSE
        PRINT 1 followed by (n - 1) zeros
ELSE
    PRINT t followed by (n - 1) zeros
```

---

## Edge Cases

* `n = 1, t = 10` → output = `-1`
* `n = 1, t = 7` → output = `7`
* `n = 2, t = 10` → output = `10`
* Largest input: `n = 9, t = 9` → `900000000`

---

## Time and Space Complexity

* **Time Complexity:** `O(n)` - printing the digits
* **Space Complexity:** `O(1)` - excluding output

---

## Java Code

```java
import java.io.*;
import java.util.StringTokenizer;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        int n = Integer.parseInt(st.nextToken());
        int t = Integer.parseInt(st.nextToken());

        if (t == 10) {
            if (n == 1) {
                System.out.println(-1);
            } else {
                System.out.print(1);
                for (int i = 0; i < n - 1; i++) {
                    System.out.print(0);
                }
            }
        } else {
            System.out.print(t);
            for (int i = 0; i < n - 1; i++) {
                System.out.print(0);
            }
        }
    }
}
```
