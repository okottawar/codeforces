# Question 118A - String Task

## Problem

Given a string, remove all vowels (`a, e, i, o, u, y`) and insert a dot `.` before each consonant.
Finally, output the resulting string in lowercase.

---

## Initial Thought Process

* Iterate through each character of the string.
* Ignore vowels.
* For consonants:
  * Add a dot `.` before them.
  * Append them to the result.
* Ensure final output is in lowercase.

---

## Insight

* Convert the entire string to lowercase at the beginning to simplify logic.
* This removes the need to handle uppercase vowels separately.
* Use a set for fast vowel lookup (`O(1)` per check).
* StringBuilder is required for efficient string construction.

---

### Algorithm

```text id="alg118a"
READ string s

CONVERT s to lowercase

FOR each character c in s:
    IF c is vowel:
        skip
    ELSE:
        append "." + c

PRINT result
```

---

## Edge Cases

* String with only vowels → output is empty.
* String with no vowels → every character gets prefixed with `.`.
* Mixed case input → handled by converting to lowercase.
* Single character input → either empty or `.x`.

---

## Time and Space Complexity

* **Time Complexity:** `O(n)` — single pass through string.
* **Space Complexity:** `O(n)` — output string storage.

---

## Java Code

```java id="code118a"
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String text = br.readLine().toLowerCase();

        Set<Character> vowels = Set.of('a', 'e', 'i', 'o', 'u', 'y');

        StringBuilder sb = new StringBuilder();

        for (int i = 0; i < text.length(); i++) {
            char c = text.charAt(i);
            if (vowels.contains(c)) continue;
            sb.append('.').append(c);
        }

        System.out.println(sb);
    }
}
```
