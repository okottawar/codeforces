# Question 41A - Translation

## Problem

Given two strings **S** and **T**, determine whether **T** is exactly the reverse of **S**.

Print:

* `"YES"` if T is the reverse of S.
* `"NO"` otherwise.

---

## Initial Thought Process

* Simply comparing both strings directly will not work.
* Since T should be the reverse of S, compare:
  * first character of S with last character of T,
  * second character of S with second last character of T,
  * and so on.
* Also, if the lengths are different, they can never be reverses.

---

## Insight

* If the lengths differ, the answer is immediately `"NO"`.
* Traverse S from left to right and T from right to left simultaneously.
* If any pair of characters doesn't match, print `"NO"`.
* If all corresponding characters match, print `"YES"`.

---

## Algorithm

```
READ S
READ T

IF length of S != length of T
    PRINT "NO"
    EXIT

FOR i = 0 to length(S) - 1
    IF S[i] != T[length(S) - 1 - i]
        PRINT "NO"
        EXIT

PRINT "YES"
```

---

## Edge Cases

* Different string lengths → NO
* Single-character strings:
  * `"a"` and `"a"` → YES
* Identical palindrome strings:
  * `"aba"` and `"aba"` → YES
* Same length but not reverses:
  * `"code"` and `"doce"` → NO

---

## Time and Space Complexity

* **Time Complexity:** `O(n)`
* **Space Complexity:** `O(1)`

---

## Java Code

```java
import java.io.*;

public class Main {
    public static void main (String [] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String s = br.readLine();
        String t = br.readLine();

        if (s.length() != t.length()) {
            System.out.println("NO");
            return;
        }

        for (int i = 0, j = s.length() - 1; i < s.length() && j >= 0; i++, j--) {
            if (s.charAt(i) != t.charAt(j)) {
                System.out.println("NO");
                return;
            }
        }

        System.out.println("YES");
    }
}
```
