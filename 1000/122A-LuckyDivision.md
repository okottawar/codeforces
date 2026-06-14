# Question 122A - Lucky Division

## Problem

A number is called **lucky** if it consists only of digits `4` and `7`.

A number is called **almost lucky** if it is divisible by at least one lucky number.

Given an integer `n`, determine whether it is **almost lucky**.

---

## Initial Thought Process

* We need to check if `n` is divisible by any number made only of digits `4` and `7`.
* Instead of generating all possible numbers dynamically, we can:

  * List all lucky numbers up to the constraint limit (`n ≤ 1000`)
  * Check divisibility one by one

---

## Insight

* This is a **divisibility checking problem over a small fixed set**.
* The total number of lucky numbers ≤ 1000 is very small (only 14).
* So brute force checking is optimal.
* No need for complex recursion in this problem.

---

## Algorithm (Optimal Approach)

```text id="alg122a"
DEFINE lucky_numbers = [4, 7, 44, 47, 74, 77,
                        444, 447, 474, 477,
                        744, 747, 774, 777]

FOR each x in lucky_numbers:
    IF n % x == 0:
        PRINT "YES"
        STOP

PRINT "NO"
```

---

## Edge Cases

* `n` itself is a lucky number → YES
* `n = 1` → NO (not divisible by any lucky number)
* `n < 4` → always NO
* `n = 1000` → still handled by same set
* Large gaps in divisibility → irrelevant, only exact divisors matter

---

## Time and Space Complexity

* **Time Complexity:** `O(1)` (fixed 14 checks)
* **Space Complexity:** `O(1)`

---

## Java Code (Optimal Pattern)

```java id="code122a"
import java.io.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int n = Integer.parseInt(br.readLine());

        int[] lucky = {
            4, 7,
            44, 47, 74, 77,
            444, 447, 474, 477,
            744, 747, 774, 777
        };

        for (int x : lucky) {
            if (n % x == 0) {
                System.out.println("YES");
                return;
            }
        }

        System.out.println("NO");
    }
}
```

---

## Recursive / Backtracking Idea (Generalized Concept)

If the constraints were larger and we could not hardcode, we generate lucky numbers using recursion.

### Idea

* Build numbers digit by digit
* At each step, choose:

  * `4`
  * `7`
* Stop when number exceeds limit (e.g., > 1000)

---

### Recursive Algorithm

```text id="rec122a"
FUNCTION generate(current):

    IF current > 1000:
        RETURN

    IF current != 0 AND n % current == 0:
        PRINT "YES"
        STOP PROGRAM

    generate(current * 10 + 4)
    generate(current * 10 + 7)
```

---

## Why Recursion Works

* Each number is built as a **binary decision tree**

  * choose 4
  * choose 7
* Depth corresponds to number length
* Total nodes remain small due to pruning (≤ 1000 constraint)

---

## Key Learning

* For small fixed constraints → brute force list is best
* For scalable generation → recursion/backtracking is the general pattern
* Both approaches rely on the same idea: **systematic generation of valid states**

---
