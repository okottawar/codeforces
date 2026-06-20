# Question 1791D - Distinct Split

## Problem

Given a string `s` of length `n`, split it into two **non-empty** parts.

For a split position `i`:

```text id="split1791d"
left = s[0...i]
right = s[i+1...n-1]
```

Let:

```text id="good1791d"
score = distinct(left) + distinct(right)
```

Find the maximum possible score among all valid splits.

---

## Initial Thought Process

* For every split, we need the number of distinct characters on both sides.
* Recomputing these counts for every position would be `O(n²)`.
* We need a way to reuse previously computed information.

---

## Insight

* Build a **prefix array** where `pref[i]` stores the number of distinct characters in `s[0...i]`.
* Build a **suffix array** where `suff[i]` stores the number of distinct characters in `s[i...n-1]`.
* Then for a split after index `i`:

```text id="ins1791d"
score = pref[i] + suff[i+1]
```

* Check all split positions and take the maximum.

---

## Algorithm

```text id="alg1791d"
Build pref[i] = distinct characters in s[0...i]

Build suff[i] = distinct characters in s[i...n-1]

answer = 0

FOR i from 0 to n-2:
    answer = max(answer,
                 pref[i] + suff[i+1])

PRINT answer
```

---

## Edge Cases

* All characters same → answer is `2`
* All characters distinct → answer is `n`
* Minimum length string (`n = 2`)
* Both parts must remain non-empty

---

## Time and Space Complexity

* **Time Complexity:** `O(n)`
* **Space Complexity:** `O(n)`

---

## Java Code

```java id="code1791d"
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        int t = Integer.parseInt(br.readLine());

        StringBuilder ans = new StringBuilder();

        while (t-- > 0) {
            int n = Integer.parseInt(br.readLine());
            String s = br.readLine();

            int[] pref = new int[n];
            int[] suff = new int[n];

            boolean[] seen = new boolean[26];
            int distinct = 0;

            for (int i = 0; i < n; i++) {
                int idx = s.charAt(i) - 'a';

                if (!seen[idx]) {
                    seen[idx] = true;
                    distinct++;
                }

                pref[i] = distinct;
            }

            Arrays.fill(seen, false);
            distinct = 0;

            for (int i = n - 1; i >= 0; i--) {
                int idx = s.charAt(i) - 'a';

                if (!seen[idx]) {
                    seen[idx] = true;
                    distinct++;
                }

                suff[i] = distinct;
            }

            int res = 0;

            for (int i = 0; i < n - 1; i++) {
                res = Math.max(res, pref[i] + suff[i + 1]);
            }

            ans.append(res).append('\n');
        }

        System.out.print(ans);
    }
}
```
