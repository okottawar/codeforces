# Question 579A - Raising Bacteria

## Problem

Given an integer **n**, representing the desired number of bacteria, determine the **minimum energy** required to obtain exactly `n` bacteria.

You can perform the following operations:

* Add **one bacterium** (costs **1 unit of energy**)
* Double the number of **all existing bacteria** (costs **0 energy**)

---

## Initial Thought Process

* At first, it seems like the sequence of additions and doublings must be simulated
* Doubling is free, so it should be used as often as possible
* The challenge is determining **when** a new bacterium must be added
* Observing the binary representation of sample inputs suggests a relationship with the number of set bits

---

## Insight

* The process starts with **0 bacteria**, so the very first bacterium must be created using the "add one" operation
* Working **backwards** from `n`:

  * If `n` is **even**, the last operation could have been a doubling → divide by 2
  * If `n` is **odd**, the last operation **must** have been adding one bacterium → subtract 1
* Every subtraction corresponds to one paid "add one bacterium" operation
* The number of such subtractions is exactly the **number of set bits (1s)** in the binary representation of `n`
* This quantity is known as the **Population Count (Popcount)** or **Hamming Weight**

---

## Algorithm

```
INPUT n

PRINT bitCount(n)
```

---

## Edge Cases

* n = 1 → output = 1
* n is a power of two (2, 4, 8, ...) → output = 1
* n is odd → at least one addition is required at the end
* n with all bits set (7, 15, 31, ...) → output equals the number of bits

---

## Time and Space Complexity

* **Time Complexity:** `O(1)` (using `Integer.bitCount()`)
* **Space Complexity:** `O(1)`

> **Note:** If counting bits manually by converting to a binary string, the complexity becomes **O(log n)**.

---

## Java Code

```java
import java.io.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int n = Integer.parseInt(br.readLine());
        System.out.println(Integer.bitCount(n));
    }
}
```
