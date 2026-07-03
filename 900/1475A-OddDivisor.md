# Question 1475A - Odd Divisor

## Problem

Given an integer `n`, determine whether it has an **odd divisor greater than 1**.

Print `"YES"` if such a divisor exists, otherwise print `"NO"`.

---

## Initial Thought Process

* The problem is about divisors, but checking all divisors is too slow for large `n`.
* We need a property of numbers that avoids factorization.

---

## Insight

Any number can be written as:

```
n = 2^k × m
```

where `m` is odd.

* If `m > 1`, then `n` has an odd divisor greater than 1 → `"YES"`
* If `m = 1`, then `n` is a pure power of 2 → `"NO"`

So the problem reduces to checking whether `n` is a **power of 2**.

---

### Key Observation

A number is a power of 2 if:

```
n & (n - 1) == 0
```

This works because powers of 2 have exactly one set bit in binary form.

---

### Algorithm

```text id="alg1475a"
READ t

REPEAT t times
    READ n

    IF n is a power of 2
        PRINT "NO"
    ELSE
        PRINT "YES"
```

---

## Edge Cases

* `n = 1` → NO (no odd divisor greater than 1)
* `n = 2, 4, 8, 16...` → NO
* Any number with an odd factor > 1 → YES

---

## Time and Space Complexity

* **Time Complexity:** `O(1)` per test case
* **Space Complexity:** `O(1)`

---

## Java Code

```java id="code1475a"
import java.io.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        int t = Integer.parseInt(br.readLine());

        while (t-- > 0) {
            long n = Long.parseLong(br.readLine());

            if (n > 0 && (n & (n - 1)) == 0) {
                System.out.println("NO");
            } else {
                System.out.println("YES");
            }
        }
    }
}
```
