# Question 577A - Multiplication Table

## Problem

Given two integers `n` and `k`, count how many pairs `(i, j)` exist such that:

```text
1 ≤ i ≤ n
1 ≤ j ≤ n
i * j = k
```

---

## Initial Thought Process

* We need to find all occurrences of `k` in an `n × n` multiplication table.
* Brute force would check all `(i, j)` pairs.
* That would be `O(n²)`, which is unnecessary.
* We need a way to reduce the search space.

---

## Insight

* For a fixed `i`, the value of `j` is uniquely determined:

```text
i * j = k  →  j = k / i
```

* So instead of iterating over all `j`, we only check one possible value.
* A pair `(i, j)` is valid only if:

```text
k % i == 0
j = k / i
1 ≤ j ≤ n
```

---

## Algorithm

```text
READ n, k

SET count = 0

FOR i from 1 to n
    IF k % i == 0
        j = k / i
        IF j ≤ n
            count++

PRINT count
```

---

## Edge Cases

* `k > n * n` → answer is `0`
* `k = 1` → only `(1,1)` is valid
* `k` is prime → very few valid pairs
* `i = k` but `k > n` → invalid automatically

---

## Time and Space Complexity

* **Time Complexity:** `O(n)`
* **Space Complexity:** `O(1)`

---

## Java Code

```java
import java.io.*;
import java.util.StringTokenizer;

public class Main {
    public static void main(String [] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        int n = Integer.parseInt(st.nextToken());
        int k = Integer.parseInt(st.nextToken());

        int count = 0;

        for(int i = 1; i <= n; i++) {
            if (k % i == 0) {
                int j = k / i;
                if (j <= n) count++;
            }
        }
        System.out.println(count);
    }
}
```
