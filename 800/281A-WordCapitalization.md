# Question 281A - Word Capitalization

## Problem

Given a non-empty word, capitalize its first letter and output the resulting word.

---

## Initial Thought Process

* Check whether the first character is a lowercase English letter.
* If it is lowercase, convert it to uppercase and concatenate it with the remaining substring.
* Otherwise, the word is already correctly capitalized, so it can be printed as-is.

---

## Insight

* Java provides the built-in method `Character.toUpperCase()`, which directly converts a character to its uppercase form.
* Using this method makes the implementation simpler and more readable than manually checking ASCII ranges.

---

### Algorithm

```text id="alg281a"
READ string s

CONVERT first character to uppercase

PRINT uppercase first character + remaining substring
```

---

## Edge Cases

* Word already starts with an uppercase letter → output remains unchanged.
* Word consists of a single character → only that character is converted and printed.
* Word starts with a lowercase letter → first character is capitalized.

---

## Time and Space Complexity

* **Time Complexity:** `O(n)` - Creating `s.substring(1)` requires copying the remaining characters.

* **Space Complexity:** `O(n)` - A new string is created for the output.

---

## Java Code

```java id="code281a"
import java.io.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String s = br.readLine();

        s = Character.toUpperCase(s.charAt(0)) + s.substring(1);
        System.out.println(s);
    }
}
```
