# Codeforces 755A - PolandBall and Hypothesis

## Problem

Given:

* An integer `n`.
* Find the smallest positive integer `m` such that:
  * `n × m + 1` is **not prime**.

It is guaranteed that such an `m` always exists.

---

## Initial Thought Process

* The hypothesis claims that numbers of the form `n × m + 1` are prime.
* To disprove it, we only need to find a single counterexample.
* So, start with `m = 1` and keep increasing it.
* As soon as `n × m + 1` becomes composite, print that `m`.

---

## Insight

* There is no mathematical trick required because the constraints are very small.
* For each value of `m`:
  * Compute `value = n × m + 1`.
  * Check whether `value` is prime.
* The first time the number is not prime, we've found the required answer.

---

## Algorithm

```text
READ n

FOR m = 1 indefinitely
    value = n × m + 1

    IF value is not prime
        PRINT m
        STOP
```

### Prime Check

```text
IF value < 2
    RETURN false

FOR i = 2 TO √value
    IF value is divisible by i
        RETURN false

RETURN true
```

---

## Edge Cases

* `m = 1` may already produce a composite number.
* Small values of `n` work correctly since primality is checked explicitly.
* The problem guarantees that a valid answer always exists.

---

## Time and Space Complexity

* **Time Complexity:** `O(m × √(n × m))` — each candidate is checked for primality by trial division.
* **Space Complexity:** `O(1)` — only a few variables are used.

---

## Java Code

```java
import java.io.*;
import java.util.*;

public class Main {

    static boolean isPrime(int x) {
        if (x < 2) return false;

        for (int i = 2; i * i <= x; i++) {
            if (x % i == 0) {
                return false;
            }
        }

        return true;
    }

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        int n = Integer.parseInt(st.nextToken());

        for (int m = 1; ; m++) {
            int value = n * m + 1;

            if (!isPrime(value)) {
                System.out.println(m);
                return;
            }
        }
    }
}
```
