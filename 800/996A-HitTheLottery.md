# Question 996A - Hit the Lottery

## Problem

Given an integer `n` representing the amount of money, find the **minimum number of bills** needed to pay exactly that amount.

Available bill denominations are:

* `100`
* `20`
* `10`
* `5`
* `1`

---

## Initial Thought Process

* Always use the largest bill possible.
* After taking as many of that bill as possible, reduce the remaining amount.
* Repeat for the next smaller denomination.

---

## Insight

* Since every denomination is a multiple or combination of smaller ones, a **greedy approach** always produces the minimum number of bills.
* At each step:

  * Add `balance / bill` to the answer.
  * Update the remaining balance using `balance %= bill`.

---

## Algorithm

```text
READ balance

SET answer = 0
SET bills = [100, 20, 10, 5, 1]

FOR each bill in bills
    answer += balance / bill
    balance = balance % bill

PRINT answer
```

---

## Edge Cases

* `n = 1` → answer is `1`
* `n` is exactly a bill denomination → answer is `1`
* Remaining balance becomes `0` before reaching the smallest denomination

---

## Time and Space Complexity

* **Time Complexity:** `O(1)` (only 5 denominations are checked)
* **Space Complexity:** `O(1)`

---

## Java Code

```java
import java.io.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        int balance = Integer.parseInt(br.readLine());

        int numBills = 0;
        int[] bills = {100, 20, 10, 5, 1};

        for (int bill : bills) {
            numBills += balance / bill;
            balance %= bill;
        }

        System.out.println(numBills);
    }
}
```
