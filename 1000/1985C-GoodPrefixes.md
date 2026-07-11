# Question 1985C - Good Prefixes

## Problem

For each test case, you are given an array.

A prefix is called **good** if there exists an element in that prefix that is equal to the sum of all the other elements in the same prefix.

Count how many prefixes are good.

---

## Initial Thought Process

* Process the array from left to right since every prefix is built incrementally.
* Keep track of the prefix sum.
* Also maintain the maximum element seen so far.
* Check whether the maximum element equals the sum of all remaining elements.

---

## Insight

* Let:
  * `sum` = sum of the current prefix
  * `max` = maximum element in the current prefix
* A prefix is good only if the largest element is the one equal to the sum of the others.
* This condition becomes:

  `max = sum - max`

* Rearranging,

  `2 × max = sum`

* Therefore, for every prefix, simply check whether `2 * max == sum`.

---

## Algorithm

```text id="alg1985c"
READ t

REPEAT t times
    READ n
    READ array

    sum = 0
    max = 0
    answer = 0

    FOR each element x
        sum += x
        max = max(max, x)

        IF 2 * max == sum
            answer++

    PRINT answer
```

---

## Edge Cases

* First element is `0` → prefix is good since `0 = 0`.
* Single positive element → cannot be good.
* Multiple maximum values → condition still works correctly.
* Large values → use `long` for the prefix sum.

---

## Time and Space Complexity

* **Time Complexity:** `O(n)` — each element is processed once.
* **Space Complexity:** `O(1)` — only a few variables are maintained.

---

## Java Code

```java id="code1985c"
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int t = Integer.parseInt(br.readLine());

        while (t-- > 0) {
            int n = Integer.parseInt(br.readLine());
            StringTokenizer st = new StringTokenizer(br.readLine());

            long sum = 0;
            long max = 0;
            int ans = 0;

            for (int i = 0; i < n; i++) {
                long x = Long.parseLong(st.nextToken());
                sum += x;
                max = Math.max(max, x);

                if (2 * max == sum) {
                    ans++;
                }
            }

            System.out.println(ans);
        }
    }
}
```
