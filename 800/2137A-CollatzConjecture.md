# Question 2137A - Collatz Conjecture

## Problem

For each test case, you are given:

* `k` — the number of Collatz operations performed
* `x` — the final value after those operations

Recall that one Collatz operation is:

* If the current number is even, divide it by `2`.
* Otherwise, replace it with `3x + 1`.

Your task is to output **any possible initial value** that becomes `x` after exactly `k` operations.

---

## Initial Thought Process

* Simulating the Collatz process backwards seems difficult because there are two possible reverse operations.
* However, we only need **one valid starting value**, not necessarily the original one.
* Look for a reverse operation that is always valid.

---

## Insight

* One reverse operation is always possible:
  * If the previous number was `2x`, then after one Collatz operation it becomes `x` (since `2x` is always even).
* Therefore, we can repeatedly apply this reverse operation `k` times.
* After `k` reverse steps, the initial value becomes:

  `x × 2^k`

* In Java, multiplying by `2^k` is simply:

  `x << k`

This always constructs a valid starting number.

---

## Algorithm

```text id="alg2137a"
READ t

REPEAT t times
    READ k, x

    PRINT (x << k)
```

---

## Edge Cases

* `k = 0` → answer is simply `x`.
* `x = 1` → answer becomes `2^k`.
* Since `k, x ≤ 20`, the result easily fits within a 32-bit integer.

---

## Time and Space Complexity

* **Time Complexity:** `O(1)` per test case.
* **Space Complexity:** `O(1)`.

---

## Java Code

```java id="code2137a"
import java.io.*;
import java.util.StringTokenizer;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        int t = Integer.parseInt(br.readLine());

        while (t-- > 0) {
            StringTokenizer st = new StringTokenizer(br.readLine());

            int k = Integer.parseInt(st.nextToken());
            int x = Integer.parseInt(st.nextToken());

            System.out.println(x << k);
        }
    }
}
```
