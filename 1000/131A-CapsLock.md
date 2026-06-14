# Question 131A - Caps Lock

## Problem

A word was typed with the **Caps Lock key accidentally turned on**.

A word is considered incorrectly typed if:

* All letters are uppercase, OR
* All letters except the first are uppercase.

In such cases, we must **invert the case of every character**:

* Uppercase → lowercase
* Lowercase → uppercase

Otherwise, leave the word unchanged.

Print the corrected word.

---

## Initial Thought Process

* The transformation should happen only in two situations:

  * Entire string is uppercase.
  * First character is lowercase and all remaining characters are uppercase.
* Both conditions can be checked by verifying whether every character from index `1` onward is uppercase.
* If the condition holds, toggle the case of every character.
* Otherwise, print the original string.

---

## Insight

* The key observation is that the decision depends only on characters from index `1` onward.
* If every character after the first is uppercase:

  * Either the whole string is uppercase (`LOCK`)
  * Or only the first character is lowercase (`cAPS`)
* In both cases, toggling every character produces the correct answer.

---

### Algorithm

```text id="alg131a"
READ string s

SET valid = true

FOR i from 1 to length(s)-1:
    IF s[i] is lowercase:
        valid = false
        BREAK

IF valid:
    TOGGLE case of every character in s
    PRINT modified string
ELSE:
    PRINT s
```

---

## Edge Cases

* Single lowercase character: `"c"` → `"C"`
* Single uppercase character: `"C"` → `"c"`
* Entire string uppercase: `"LOCK"` → `"lock"`
* First lowercase, rest uppercase: `"cAPS"` → `"Caps"`
* Mixed casing: `"Codeforces"` → unchanged

---

## Time and Space Complexity

* **Time Complexity:** `O(n)` - one pass to validate and one pass to toggle
* **Space Complexity:** `O(n)` - output string is constructed using `StringBuilder`

---

## Java Code

```java id="code131a"
import java.io.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String s = br.readLine();

        boolean valid = true;

        for (int i = 1; i < s.length(); i++) {
            if (Character.isLowerCase(s.charAt(i))) {
                valid = false;
                break;
            }
        }

        if (valid) {
            StringBuilder ans = new StringBuilder();

            for (int i = 0; i < s.length(); i++) {
                char ch = s.charAt(i);

                if (Character.isUpperCase(ch)) {
                    ans.append(Character.toLowerCase(ch));
                } else {
                    ans.append(Character.toUpperCase(ch));
                }
            }

            System.out.println(ans);
        } else {
            System.out.println(s);
        }
    }
}
```
