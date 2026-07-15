# Codeforces 34B - Sale

## Problem

Given:

* `n` TVs, where each TV has a price.
* A **negative** price means the store pays you to take the TV.
* You can take **at most `m` TVs**.

Find the maximum amount of money you can earn.

---

## Initial Thought Process

* Positive-priced TVs reduce your earnings, so they should never be taken.
* Negative-priced TVs increase your earnings.
* Since you can take at most `m` TVs, choose the most negative prices.

---

## Insight

* Sort the prices in ascending order.
* After sorting:

  * Negative prices appear first.
  * The most profitable TVs are the smallest (most negative) values.
* Traverse the first `m` elements:

  * If the price is negative, add its absolute value to the answer.
  * Stop as soon as a non-negative price is encountered.

---

## Algorithm

```text id="alg34b"
READ n, m

READ array prices

SORT prices

answer = 0

FOR i = 0 to min(n, m) - 1
    IF prices[i] < 0
        answer += -prices[i]
    ELSE
        BREAK

PRINT answer
```

---

## Edge Cases

* No negative prices → answer is `0`.
* All prices are negative → take the `m` most negative TVs.
* Number of negative prices is less than `m` → take only the negative ones.
* `m = 0` → answer is `0`.

---

## Time and Space Complexity

* **Time Complexity:** `O(n log n)` — sorting dominates the runtime.
* **Space Complexity:** `O(1)` — only the input array is used (excluding input storage).

---

## Java Code

```java id="code34b"
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        int n = Integer.parseInt(st.nextToken());
        int m = Integer.parseInt(st.nextToken());

        int[] prices = new int[n];
        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < n; i++) {
            prices[i] = Integer.parseInt(st.nextToken());
        }

        Arrays.sort(prices);

        int answer = 0;
        for (int i = 0; i < Math.min(n, m); i++) {
            if (prices[i] < 0) {
                answer += -prices[i];
            } else {
                break;
            }
        }

        System.out.println(answer);
    }
}
```
