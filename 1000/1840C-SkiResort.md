# Codeforces 1840C - Ski Resort

## Problem

Given an array `a` of length `n`, count the number of contiguous segments such that:

* Segment length is at least `k`
* Every element in the segment is at most `q`

---

## Initial Thought Process

* Any value greater than `q` breaks a valid segment.
* So we only need to consider consecutive blocks where all values are `<= q`.
* For each such block, count how many subarrays have length at least `k`.

---

## Insight

Let a valid block have length `len`.

If `len >= k`, the number of valid subarrays inside it is: `x = len - k + 1`

The possible starting positions contribute: `x + (x - 1) + ... + 1`

which equals: `x * (x + 1) / 2`

So each valid block contributes: `(len - k + 1) * (len - k + 2) / 2` to the answer.

---

### Algorithm

```text
ans = 0
len = 0

FOR each element:

    IF value <= q:
        len++

    ELSE:
        process current block
        len = 0

Process the final block if needed

PRINT ans
```

Where processing a block means:

```text
IF len >= k:
    x = len - k + 1
    ans += x * (x + 1) / 2
```

---

## Edge Cases

* No valid block of length `k`
* Entire array forms one valid block
* Block length exactly `k` contributes `1`

---

## Time and Space Complexity

* **Time Complexity:** `O(n)`
* **Space Complexity:** `O(1)`

---

## Java Code

```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        int t = Integer.parseInt(br.readLine());

        while (t-- > 0) {
            StringTokenizer st = new StringTokenizer(br.readLine());

            int n = Integer.parseInt(st.nextToken());
            int k = Integer.parseInt(st.nextToken());
            int q = Integer.parseInt(st.nextToken());

            st = new StringTokenizer(br.readLine());

            long ans = 0;
            int len = 0;

            for (int i = 0; i < n; i++) {
                int a = Integer.parseInt(st.nextToken());

                if (a <= q) {
                    len++;
                } else {
                    if (len >= k) {
                        long x = len - k + 1;
                        ans += x * (x + 1) / 2;
                    }
                    len = 0;
                }
            }

            if (len >= k) {
                long x = len - k + 1;
                ans += x * (x + 1) / 2;
            }

            System.out.println(ans);
        }
    }
}
```
