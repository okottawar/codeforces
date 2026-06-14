# Question 479A - Expression

## Problem

Given three integers `a`, `b`, and `c`, you can insert `+`, `*`, and parentheses in any way (without changing the order of numbers).

You must find the **maximum possible value**.

---

## Initial Thought Process

* We need to evaluate all possible valid expressions formed using `a`, `b`, and `c`.
* Parentheses change evaluation order, so grouping matters.
* Since there are only 3 numbers, the number of possible expressions is small.
* We can brute force all valid cases and take the maximum.

---

## Insight

* This is a **brute-force expression evaluation problem** with very small constraints.
* No need for parsing or recursion.
* We only consider distinct parenthesization structures.
* Operator precedence reduces the need for some cases.

---

## Key Observation

For 3 numbers, only a few unique evaluation patterns matter:

* All addition
* All multiplication
* Mixed grouping with parentheses affecting order

We evaluate all possible meaningful combinations and take the maximum.

---

## Algorithm 

```text id="alg479a"
SET maxResult = 0

EVALUATE all valid expressions:
    a + b + c
    a * b * c
    (a + b) * c
    a * (b + c)    

UPDATE maxResult with maximum of all values

PRINT maxResult
```

---

## Edge Cases

* All numbers equal → any grouping gives same result
* Presence of `1` changes multiplication behavior significantly
* Small values → addition may dominate
* Large multiplication chains → multiplication dominates

---

## Time and Space Complexity

* **Time Complexity:** `O(1)` — constant number of expressions
* **Space Complexity:** `O(1)`

---

## Java Code

```java id="code479a"
import java.io.*;
import java.util.StringTokenizer;

public class Main {
    public static void main(String [] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        
        int a = Integer.parseInt(st.nextToken());
        int b = Integer.parseInt(st.nextToken());
        int c = Integer.parseInt(st.nextToken());
        int maxResult = 0;
        
        maxResult = Math.max(maxResult, a + b + c);
        maxResult = Math.max(maxResult, a * b * c);
        maxResult = Math.max(maxResult, (a + b) * c);
        maxResult = Math.max(maxResult, a * (b + c));
        
        System.out.println(maxResult);
    }
}
```
