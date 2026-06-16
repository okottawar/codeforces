# Question 1913B - Swap and Delete

## Problem

You are given a binary string `s` consisting of `0` and `1`.

You can perform two operations:

* **Delete** any character (cost = 1 coin)
* **Swap** any two characters (cost = 0 coins)

After operations, you obtain a string `t`.

The string `t` is called **good** if for every position `i`:

* `t[i] != s[i]` (compared with the original string)

Your task is to find the **minimum cost** to make `t` good.

---

## Initial Thought Process

* Swaps are free → we can rearrange any chosen characters arbitrarily.
* Deletion is the only costly operation.
* So the problem becomes:
  **Keep as many characters as possible such that we can permute them to avoid matching original positions.**

We need to decide how many characters to keep; the rest are deleted.

---

## Insight

* Since swapping is free, we only care about counts of `0` and `1`.
* We try to match characters of `s` with opposite available characters.
* If at some position we cannot place a different character, we must delete remaining suffix.
* This leads to a greedy simulation:

  * Maintain remaining `zeros` and `ones`
  * Scan left to right and "consume" opposite characters
  * If impossible, delete remaining part

---

### Key Idea

We try to construct `t` implicitly:

* At index `i`, we need a character different from `s[i]`
* If `s[i] == '0'`, we need a `1` available
* If `s[i] == '1'`, we need a `0` available

If not possible → we delete all remaining characters.

---

### Algorithm

```text id="alg1913b"
COUNT zeros and ones in s
INITIALIZE res = 0

FOR each index i in s:
    IF s[i] == '0':
        IF ones == 0:
            res = n - i
            BREAK
        ones--

    ELSE:
        IF zeros == 0:
            res = n - i
            BREAK
        zeros--

PRINT res
```

---

## Edge Cases

* All characters same (e.g., `0000`) → must delete all
* Already balanced and rearrangeable → cost = 0
* Small strings (length 1 or 2) → often need deletion
* Early failure vs late failure affects cost

---

## Time and Space Complexity

* **Time Complexity:** `O(n)` per test case (single pass)
* **Space Complexity:** `O(1)` extra space

---

## Java Code

```java id="java1913b"
import java.io.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        int t = Integer.parseInt(br.readLine().trim());

        while (t-- > 0) {
            String s = br.readLine().trim();
            int n = s.length();

            int zeros = 0, ones = 0;

            for (int i = 0; i < n; i++) {
                if (s.charAt(i) == '0') zeros++;
                else ones++;
            }

            int res = 0;

            for (int i = 0; i < n; i++) {
                char c = s.charAt(i);

                if (c == '0') {
                    if (ones == 0) {
                        res = n - i;
                        break;
                    }
                    ones--;
                } else {
                    if (zeros == 0) {
                        res = n - i;
                        break;
                    }
                    zeros--;
                }
            }

            System.out.println(res);
        }
    }
}
```
