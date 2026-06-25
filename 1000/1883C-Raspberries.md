# Codeforces 1883C - Raspberries

## Problem

Given an array `a` and an integer `k` (`2 ≤ k ≤ 5`).

In one operation, you may choose any element and increase it by `1`.

Find the minimum number of operations required so that the product of all elements becomes divisible by `k`.

---

## Initial Thought Process

* The statement talks about the product of the entire array.
* Directly computing or modifying the product is unnecessary.
* Since `k` is very small (`2, 3, 4, 5`), we can analyze each case separately.
* Divisibility of a product depends on the prime factors contributed by the elements.

---

## Insight

### Case 1: `k = 2, 3, 5`

The product is divisible by `k` if at least one element is divisible by `k`.

For each element:

```text
cost = (k - a[i] % k) % k
```

This gives the number of increments needed to make `a[i]` divisible by `k`.

The answer is simply the minimum such cost.

---

### Case 2: `k = 4`

A product is divisible by `4` if it contains at least two factors of `2`.

This can happen in two ways:

#### Option 1

Make some element divisible by `4`.

Cost:

```text
min((4 - a[i] % 4) % 4)
```

---

#### Option 2

Ensure there are at least two even numbers.

Count:

```text
evenCount = number of even elements
```

Then:

```text
evenCount >= 2  -> cost = 0
evenCount == 1  -> cost = 1
evenCount == 0  -> cost = 2
```

because every odd number becomes even with exactly one increment.

Take the minimum of the two options.

---

### Algorithm

```text
IF k != 4:

    ans = INF

    FOR each element:
        ans = min(ans, (k - a[i] % k) % k)

ELSE:

    makeDiv4 = INF
    evenCount = 0

    FOR each element:

        makeDiv4 = min(
            makeDiv4,
            (4 - a[i] % 4) % 4
        )

        IF a[i] is even:
            evenCount++

    IF evenCount >= 2:
        makeTwoEvens = 0

    ELSE IF evenCount == 1:
        makeTwoEvens = 1

    ELSE:
        makeTwoEvens = 2

    ans = min(makeDiv4, makeTwoEvens)

PRINT ans
```

---

## Edge Cases

* Product already divisible by `k`
* `k = 4` and there are already two even numbers
* `k = 4` and one element is already divisible by `4`
* All elements are odd
* Array contains only one element

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
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        int t = Integer.parseInt(br.readLine());

        while (t-- > 0) {
            StringTokenizer st = new StringTokenizer(br.readLine());

            int n = Integer.parseInt(st.nextToken());
            int k = Integer.parseInt(st.nextToken());

            int[] arr = new int[n];

            st = new StringTokenizer(br.readLine());
            for (int i = 0; i < n; i++) {
                arr[i] = Integer.parseInt(st.nextToken());
            }

            int ans;

            if (k != 4) {
                ans = Integer.MAX_VALUE;

                for (int x : arr) {
                    ans = Math.min(ans, (k - x % k) % k);
                }
            } else {
                int makeDiv4 = Integer.MAX_VALUE;
                int evenCount = 0;

                for (int x : arr) {
                    makeDiv4 = Math.min(makeDiv4, (4 - x % 4) % 4);

                    if (x % 2 == 0) {
                        evenCount++;
                    }
                }

                int makeTwoEvens;

                if (evenCount >= 2) {
                    makeTwoEvens = 0;
                } else if (evenCount == 1) {
                    makeTwoEvens = 1;
                } else {
                    makeTwoEvens = 2;
                }

                ans = Math.min(makeDiv4, makeTwoEvens);
            }

            System.out.println(ans);
        }
    }
}
```
