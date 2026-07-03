# Question 977A - Wrong Subtraction

## Problem

Given an integer `n`, perform the following operation exactly `k` times:

* If the last digit of `n` is `0`, divide it by `10`.
* Otherwise, subtract `1` from it.

Print the final value of `n`.

---

## Initial Thought Process

* Each operation depends only on the last digit of the current number.
* Simulate the process for exactly `k` iterations.

---

## Insight

For each operation:

* If the last digit is `0`, removing it is equivalent to dividing the number by `10`.
* Otherwise, decrement the number by `1`.

Repeating this process `k` times gives the required answer.

---

### Algorithm

```text id="alg977a"
READ n, k

REPEAT k times
    IF n % 10 == 0
        n = n / 10
    ELSE
        n = n - 1

PRINT n
```

---

## Edge Cases

* `n` ends with `0` → divide by `10`.
* `n` does not end with `0` → subtract `1`.
* The constraints guarantee the operations are always valid.

---

## Time and Space Complexity

* **Time Complexity:** `O(k)`.
* **Space Complexity:** `O(1)`.

---

## Java Code

```java id="code977a"
import java.io.*;
import java.util.StringTokenizer;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        int n = Integer.parseInt(st.nextToken());
        int k = Integer.parseInt(st.nextToken());

        while (k-- > 0) {
            if (n % 10 == 0) {
                n /= 10;
            } else {
                n--;
            }
        }

        System.out.println(n);
    }
}
```
