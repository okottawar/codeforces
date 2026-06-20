# Question 1690D - Black and White Stripe

## Problem

You are given a string `s` of length `n` consisting of:
* `'B'` → black tile
* `'W'` → white tile

You are also given an integer `k`.
You need to choose a **contiguous substring of length `k`** and repaint all tiles in it to black.

Find the minimum number of tiles that need to be repainted.

---

## Initial Thought Process

* We must pick a window of size `k`.
* Each `'W'` inside that window must be repainted.
* So we need to find the window with the fewest `'W'`.

---

## Insight

Instead of counting black tiles, focus on whites:

> The cost of choosing a window = number of `'W'` in that window.

So the problem reduces to:

```text id="goal"
Find minimum number of 'W' in any substring of length k
```

This is a **fixed-size sliding window** problem.

---

## Algorithm

```text id="alg1690d"
COUNT whites in first window of size k
ans = whites

FOR i from k to n-1:
    IF stripe[i - k] == 'W': decrement whites
    IF stripe[i] == 'W': increment whites

    ans = min(ans, whites)

PRINT ans
```

---

## Edge Cases

* `k = n` → answer = total number of `'W'`
* All `'B'` → answer = 0
* All `'W'` → answer = k

---

## Time and Space Complexity

* **Time Complexity:** `O(n)` per test case
* **Space Complexity:** `O(1)`

---

## Java Code

```java id="code1690d"
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

            String stripe = br.readLine();

            int whites = 0;
            for (int i = 0; i < k; i++) {
                if (stripe.charAt(i) == 'W') whites++;
            }

            int ans = whites;

            for (int i = k; i < n; i++) {
                if (stripe.charAt(i - k) == 'W') whites--;
                if (stripe.charAt(i) == 'W') whites++;
                ans = Math.min(ans, whites);
            }

            System.out.println(ans);
        }
    }
}
```
