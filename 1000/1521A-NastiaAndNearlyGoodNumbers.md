# Question 1521A - Nastia and Nearly Good Numbers

## Problem

Given two integers `a` and `b`, find three **distinct** positive integers `x`, `y`, and `z` such that:

* All three are divisible by `a`.
* `x + y = z`.
* `z` is divisible by `a × b`.

If it is impossible, print `"NO"`.

---

## Initial Thought Process

* Every required number must be a multiple of `a`.
* Instead of trying to split `a × b`, directly construct three multiples of `a` that satisfy the equation.
* The only tricky part is ensuring all three numbers are distinct.

---

## Insight

Choose:

* `x = a`
* `z = 2ab`

Then,

* `y = z - x = 2ab - a = a(2b - 1)`

So the construction is:

* `x = a`
* `y = a(2b - 1)`
* `z = 2ab`

This satisfies:

* All three are divisible by `a`.
* `x + y = z`.
* `z` is divisible by `ab`.

The only invalid case is `b = 1`, where `x = y = a`.

---

### Algorithm

```text id="alg1521a"
READ t

REPEAT t times
    READ a, b

    IF b == 1
        PRINT "NO"
    ELSE
        PRINT "YES"
        PRINT a, a * (2 * b - 1), 2 * a * b
```

---

## Edge Cases

* `b = 1` → no valid construction exists.
* Use `long` since the products can exceed the `int` range.

---

## Time and Space Complexity

* **Time Complexity:** `O(1)` per test case.
* **Space Complexity:** `O(1)`.

---

## Java Code

```java id="code1521a"
import java.io.*;
import java.util.StringTokenizer;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        int t = Integer.parseInt(br.readLine());

        while (t-- > 0) {
            StringTokenizer st = new StringTokenizer(br.readLine());

            long a = Long.parseLong(st.nextToken());
            long b = Long.parseLong(st.nextToken());

            if (b == 1) {
                System.out.println("NO");
                continue;
            }

            System.out.println("YES");
            System.out.println(a + " " + (a * (2 * b - 1)) + " " + (2 * a * b));
        }
    }
}
```
