# Question 1374B - Multiply by 2, Divide by 6

## Problem

For each test case, you are given an integer **N**.

You can perform the following operations:

1. Divide **N** by **6** if it is divisible by **6**.
2. Multiply **N** by **2** (equivalently, when **N** is divisible by **3** but not by **6**, divide by **3** first and count it as two operations).

Find the **minimum number of operations** required to make **N = 1**.

If it is impossible, print **-1**.

---

## Initial Thought Process

* The goal is to reduce the number to **1**.
* Whenever possible, dividing by **6** is the best choice since it decreases the number the fastest.
* If the number is divisible by **3** but not by **6**, it must first be transformed so that a division by **6** becomes possible.

---

## Insight

* If **N** is not divisible by **3**, it can never reach **1**.
* Priority of operations:
  * If **N % 6 == 0**, divide by **6** (1 operation).
  * Otherwise, if **N % 3 == 0**, divide by **3** and account for the required multiplication by **2** (2 operations).
* Repeat until:
  * **N = 1** → output the operation count.
  * A number not divisible by **3** is encountered → output **-1**.

---

## Algorithm

```
READ T

WHILE T > 0
    READ N
    count = 0

    WHILE N != 1
        IF N is not divisible by 3
            PRINT -1
            STOP processing this test case

        ELSE IF N is divisible by 6
            N = N / 6
            count++

        ELSE
            N = N / 3
            count += 2

    PRINT count
```

---

## Edge Cases

* N = 1 → 0 operations
* N = 6 → 1 operation
* N = 3 → 2 operations
* N = 10 → -1 (not divisible by 3)
* Numbers containing extra factors other than 2 and 3 may become impossible to reduce.

---

## Time and Space Complexity

* **Time Complexity:** `O(log n)` (each operation reduces the value of `N`)
* **Space Complexity:** `O(1)`

---

## Java Code

```java
import java.io.*;

public class Main {
    public static void main (String [] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int t = Integer.parseInt(br.readLine());

        while (t-- > 0) {
            long n = Integer.parseInt(br.readLine());

            boolean isPossible = true;
            int count = 0;

            while (n != 1) {
                if (n % 3 != 0) {
                    isPossible = false;
                    break;
                } else if (n % 6 == 0) {
                    n /= 6;
                    count++;
                } else {
                    n /= 3;
                    count += 2;
                }
            }

            if (isPossible)
                System.out.println(count);
            else
                System.out.println(-1);
        }
    }
}
```
