# Question 546A - Soldier and Bananas

## Problem

A soldier wants to buy `w` bananas.
The cost of each banana increases linearly:

* 1st banana costs `k`
* 2nd banana costs `2k`
* 3rd banana costs `3k`
* ...
* w-th banana costs `w * k`

He initially has `n` dollars.
Find how many more dollars he needs to borrow to buy all the bananas.

---

## Initial Thought Process

* The total cost is the sum of an arithmetic series multiplied by `k`.
* Instead of simulating purchases one by one, we can compute the total cost directly.
* Then subtract the soldier’s initial money `n`.

---

## Insight

* Sum of first `w` natural numbers: `(W * (W + 1) / 2)`
* So total cost becomes: `TOTAL_COST = K * (W * (W + 1) / 2)`
* The required amount to borrow is: `MAX(0, TOTAL_COST - N)`

---

### Algorithm

```text id="alg546a"
READ k, n, w

total_cost = k * (w * (w + 1) / 2)

borrow = total_cost - n

IF borrow < 0:
    borrow = 0

PRINT borrow
```

---

## Edge Cases

* If `n >= total_cost` → output `0`
* If `w = 1` → cost is just `k`
* Large `w` → must avoid overflow using `long`

---

## Time and Space Complexity

* **Time Complexity:** `O(1)`

* **Space Complexity:** `O(1)`

---

## Java Code

```java id="code546a"
import java.io.*;
import java.util.StringTokenizer;

public class Main {
    public static void main (String [] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        long k = Long.parseLong(st.nextToken());
        long n = Long.parseLong(st.nextToken());
        long w = Long.parseLong(st.nextToken());

        long totalCost = k * (w * (w + 1) / 2);
        long borrow = totalCost - n;

        System.out.println(Math.max(0, borrow));
    }
}
```
