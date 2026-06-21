# Question 160A - Twins

## Problem

Given `n` coins with different values, determine the minimum number of coins one twin must take so that the total value of their coins becomes **strictly greater** than the value of the remaining coins.

---

## Initial Thought Process

* To maximize the collected sum quickly, we should take the largest coins first.
* Sorting helps us access bigger values easily.
* Build the total sum of all coins.
* Keep taking the largest coins until our collected sum becomes greater than the remaining sum.

---

## Insight

* Taking smaller coins first may require more coins.
* Greedily choosing the largest available coin minimizes the number of coins taken.
* Once:

```text
takenSum > totalSum - takenSum
```

the condition is satisfied immediately.

---

## Algorithm

```text
READ n
READ array coins

SORT coins in increasing order

COMPUTE totalSum

SET takenSum = 0
SET count = 0

FOR i from n-1 down to 0
    takenSum += coins[i]
    count++

    IF takenSum > totalSum - takenSum
        PRINT count
        STOP
```

---

## Edge Cases

* Only one coin → answer is `1`
* All coins equal → may need more than half the coins
* Largest coin already exceeds remaining sum → answer is `1`

---

## Time and Space Complexity

* **Time Complexity:** `O(n log n)` due to sorting
* **Space Complexity:** `O(1)` excluding sorting space

---

## Java Code

```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws Exception {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int n = Integer.parseInt(br.readLine());
        int[] coins = new int[n];
        StringTokenizer st = new StringTokenizer(br.readLine());

        int totalSum = 0;

        for (int i = 0; i < n; i++) {
            coins[i] = Integer.parseInt(st.nextToken());
            totalSum += coins[i];
        }

        Arrays.sort(coins);

        int takenSum = 0;
        int count = 0;

        for (int i = n - 1; i >= 0; i--) {
            takenSum += coins[i];
            count++;
            if (takenSum > totalSum - takenSum) {
                System.out.println(count);
                return;
            }
        }
    }
}
```
