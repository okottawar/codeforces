# Question 1374C - Move Brackets

## Problem

Given a bracket sequence consisting of `'('` and `')'`, determine the **minimum number of moves** required to make it a regular bracket sequence.

A move consists of:

* Choosing any bracket
* Removing it from its current position
* Appending it to the end of the string

Example:

* `"()()"` → `0`
* `"))(("` → `2`
* `"())("` → `1`

---

## Initial Thought Process

* A valid bracket sequence should never have more closing brackets than opening brackets while scanning from left to right.
* We keep track of currently available unmatched `'('`.
* Whenever a `')'` appears:

  * If an unmatched `'('` exists, we match them.
  * Otherwise, this closing bracket is invalid and must eventually be moved.

---

## Insight

* We do not actually need to simulate moving brackets.
* Every unmatched `')'` encountered during the scan contributes exactly one required move.
* Maintain a balance representing the number of unmatched opening brackets available.
* If a closing bracket appears when balance is zero, increment the answer.

---

### Algorithm

```text id="alg1374c"
INITIALIZE balance = 0
INITIALIZE answer = 0

FOR each character c in string:

    IF c == '(':
        balance++

    ELSE:
        IF balance > 0:
            balance--
        ELSE:
            answer++

PRINT answer
```

---

## Edge Cases

* Already valid sequence → answer is `0`
* All invalid closings appear first (e.g. `"))(("`) → count all unmatched `')'`
* Nested valid brackets → handled naturally by balance tracking
* Multiple unmatched closings throughout the string → each contributes one move

---

## Time and Space Complexity

* **Time Complexity:** `O(n)` - single pass through the string
* **Space Complexity:** `O(1)` 0 only two integer variables used

---

## Java Code (Optimal Pattern)

```java id="code1374c"
import java.io.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        int t = Integer.parseInt(br.readLine());

        while (t-- > 0) {
            int n = Integer.parseInt(br.readLine());
            String s = br.readLine();

            int balance = 0;
            int ans = 0;

            for (int i = 0; i < s.length(); i++) {
                if (s.charAt(i) == '(') {
                    balance++;
                } else {
                    if (balance > 0) {
                        balance--;
                    } else {
                        ans++;
                    }
                }
            }

            System.out.println(ans);
        }
    }
}
```
