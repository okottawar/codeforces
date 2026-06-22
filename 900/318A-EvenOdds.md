# Question 318A - Even Odds

## Problem

Given two integers `n` and `k`.

Construct a sequence where:

* All odd numbers from `1` to `n` appear first.
* Then all even numbers from `1` to `n` appear.

Find the `k`-th number in this sequence.

---

## Initial Thought Process

* Generating the entire sequence is unnecessary because `n` can be as large as `10^12`.
* We only need to determine whether the `k`-th position lies in the odd section or the even section.
* Once the section is known, the value can be computed directly using a formula.

---

## Insight

* The sequence starts with all odd numbers: `1, 3, 5, ...`

* The number of odd values from `1` to `n` is: `(n + 1) / 2`

* If `k` lies within these positions, the answer is simply the `k`-th odd number: `2 × k − 1`

* Otherwise, the position belongs to the even section.

Then the answer becomes: `2 × k - oddCount`

---

## Algorithm

```text
READ n, k

oddCount = (n + 1) / 2

IF k <= oddCount
    PRINT (2 * k - 1)
ELSE
    PRINT 2 * (k - oddCount)
```

---

## Edge Cases

* `n = 1` → sequence contains only `1`
* `n` is even → odds and evens are equal in count
* `n` is odd → odds are one more than evens
* `k = 1` → answer is always `1`
* `k = n` → answer is the last even number (or last remaining number)
* Large values up to `10^12` require `long`, not `int`

---

## Time and Space Complexity

* **Time Complexity:** `O(1)`
* **Space Complexity:** `O(1)`

---

## Java Code

```java
import java.io.*;
import java.util.StringTokenizer;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        long n = Long.parseLong(st.nextToken());
        long k = Long.parseLong(st.nextToken());

        long oddCount = (n + 1) / 2;

        if (k <= oddCount) {
            System.out.println(2 * k - 1);
        } else {
            System.out.println(2 * (k - oddCount));
        }
    }
}
```
