# Question 236A - Boy or Girl

## Problem

Given a username string, determine whether the number of distinct characters is odd or even.

Print:

* `"CHAT WITH HER!"` if the number of distinct characters is even
* `"IGNORE HIM!"` if the number of distinct characters is odd

---

## Initial Thought Process

* Extract all unique characters from the string.
* Count how many distinct characters exist.
* Check whether the count is odd or even.

---

## Insight

* The problem only depends on **distinct characters**, not frequency.
* A `HashSet` can be used to automatically store unique characters.
* Final decision is based on the parity of the set size.

---

## Algorithm

```text id="alg236a"
READ username

CREATE empty set

FOR each character in username
    ADD character to set

IF size of set is even
    PRINT "CHAT WITH HER!"
ELSE
    PRINT "IGNORE HIM!"
```

---

## Edge Cases

* Single character → 1 distinct → odd → `"IGNORE HIM!"`
* All characters same → 1 distinct → odd
* All characters unique → depends on total length parity

---

## Time and Space Complexity

* **Time Complexity:** `O(n)` — iterate through string once
* **Space Complexity:** `O(1)` — at most 26 lowercase letters

---

## Java Code

```java id="code236a"
import java.io.*;
import java.util.HashSet;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        String username = br.readLine();

        HashSet<Character> set = new HashSet<>();

        for (char c : username.toCharArray()) {
            set.add(c);
        }

        if (set.size() % 2 == 0) {
            System.out.println("CHAT WITH HER!");
        } else {
            System.out.println("IGNORE HIM!");
        }
    }
}
```
