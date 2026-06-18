# Question 742A - Arpa’s Hard Exam and Mehrdad’s Naive Cheat

## Problem

Given a non-negative integer `n`, find the **last digit of** `8^n`.

Since `n` can be very large, computing the entire power is unnecessary. We only need its final digit.

Examples:

* `n = 0` → `8^0 = 1` → answer = `1`
* `n = 1` → `8` → answer = `8`
* `n = 2` → `64` → answer = `4`

---

## Initial Thought Process

* Directly computing `8^n` is impossible for large `n`.
* We only care about the last digit.
* Last digits of powers often follow a repeating cycle.

Let's observe:

```text
8^1 = 8  → 8
8^2 = 64 → 4
8^3 = 512 → 2
8^4 = 4096 → 6
8^5 → 8
```

The last digits repeat as:

```text
8, 4, 2, 6
```

with cycle length `4`.

---

## Insight

* The last digit pattern of powers of `8` repeats every `4` powers.
* The cycle is:

```text
Index: 1 2 3 4
Digit: 8 4 2 6
```

* For any `n > 0`, the required digit is:

```text
cycle[(n - 1) % 4]
```

* Special case:

  * `8^0 = 1`

---

### Algorithm

```text id="alg742a"
IF n == 0:
    PRINT 1
    STOP

cycle = [8, 4, 2, 6]

PRINT cycle[(n - 1) % 4]
```

---

## Edge Cases

* `n = 0` → answer is `1`
* `n = 1` → first element of cycle → `8`
* Very large values of `n` → still work because only modulo `4` is needed
* Multiples of `4` correctly map to digit `6`

---

## Time and Space Complexity

* **Time Complexity:** `O(1)`
* **Space Complexity:** `O(1)`

---

## Java Code

```java id="code742a"
import java.io.*;

public class Main {
    public static void main (String [] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int n = Integer.parseInt(br.readLine());

        int[] cycle = {8, 4, 2, 6};

        if (n == 0) {
            System.out.println(1);
        } else {
            System.out.println(cycle[(n - 1) % 4]);
        }
    }
}
```
