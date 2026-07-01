# Question 1744C - Traffic Light

## Problem

You are given a circular string of length `n` representing traffic lights.

Each character is one of:

* `'r'` (red)
* `'y'` (yellow)
* `'g'` (green)

Given a character `c`, determine the **maximum time** you have to wait if you start from any occurrence of `c` and move clockwise until you reach the next `'g'`.

Print the maximum waiting time.

---

## Initial Thought Process

* For every occurrence of `c`, find the next `'g'` while moving clockwise.
* Compute the distance to that `'g'`.
* The answer is the maximum of all such distances.

The difficulty is that the string is **circular**, so the next `'g'` may appear after wrapping around to the beginning.

---

## Insight

* Since the string is circular, duplicate it by concatenating it with itself.
* Now every wrap-around path becomes a normal forward traversal.
* Traverse the doubled string from **right to left**.
* Keep track of the nearest `'g'` seen so far.
* Whenever we encounter `c` in the **first `n` characters**, compute its distance to the nearest `'g'`.
* Update the maximum distance.

---

### Algorithm

```text id="alg1744c"
READ n and character c

READ string s

IF c == 'g':
    PRINT 0
    CONTINUE

DOUBLE the string:
    s = s + s

SET nextGreen = -1
SET answer = 0

FOR i from 2*n-1 down to 0:
    IF s[i] == 'g':
        nextGreen = i

    IF i < n AND s[i] == c:
        answer = max(answer, nextGreen - i)

PRINT answer
```

---

## Edge Cases

* `c = 'g'`

No waiting is required.

Answer is `0`.

* The next `'g'` is after wrapping around.

Doubling the string naturally handles this case.

* Multiple occurrences of `c`

Compute the waiting time for each occurrence and take the maximum.

* Only one occurrence of `c`

Simply calculate its distance to the next `'g'`.

---

## Time and Space Complexity

* **Time Complexity:** `O(n)` - one traversal of the doubled string.
* **Space Complexity:** `O(n)` - storing the doubled string.

---

## Java Code

```java id="code1744c"
import java.io.*;
import java.util.StringTokenizer;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int t = Integer.parseInt(br.readLine());

        while (t-- > 0) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            int n = Integer.parseInt(st.nextToken());
            char c = st.nextToken().charAt(0);
            String seq = br.readLine().repeat(2);

            if (c == 'g') {
                System.out.println(0);
                continue;
            }

            int nextG = -1;
            int ans = 0;
            for (int i = 2 * n - 1; i >= 0; i--) {
                if (seq.charAt(i) == 'g') {
                    nextG = i;
                }
                if (i < n && seq.charAt(i) == c) {
                    ans = Math.max(ans, nextG - i);
                }
            }

            System.out.println(ans);
        }
    }
}
```
