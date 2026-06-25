# Codeforces 208A - Dubstep

## Problem

The song is given as a string where the word `"WUB"` has been inserted multiple times.

Your task is to restore the original song by:

* Removing all `"WUB"` substrings
* Restoring proper word separation using single spaces

---

## Initial Thought Process

* `"WUB"` appears as a repeating pattern.
* It can be treated as noise or a separator.
* We can remove or replace `"WUB"` to reconstruct the original words.
* After removal, extra spaces may appear and must be handled.

---

## Insight

Instead of simply deleting `"WUB"`, we interpret it as a **word separator**.

So: `"WUB" → " "`


However, multiple consecutive `"WUB"` sequences may produce multiple spaces, so we must normalize spacing.

---

## Key Observation

After replacing all `"WUB"`:

* Words may be separated by multiple spaces
* There may be leading/trailing spaces

So we must:

1. Replace all `"WUB"` with a space
2. Collapse multiple spaces into one logical separation
3. Trim leading and trailing spaces

---

## Algorithm

```text id="a1"
READ string s

REPLACE all occurrences of "WUB" with " "

TRIM leading and trailing spaces

OUTPUT result
```

More precisely:

```text id="alg208a"
s = s.replaceAll("(WUB)+", " ")
s = s.trim()
print s
```

---

## Edge Cases

* String starts with `"WUB"`
* String ends with `"WUB"`
* Multiple consecutive `"WUB"` blocks
* No `"WUB"` present at all
* Entire string consists of `"WUB"`

---

## Time and Space Complexity

* **Time Complexity:** `O(n)` - regex over string
* **Space Complexity:** `O(n)`

---

## Java Code

```java id="java208a"
import java.io.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String record = br.readLine();
        record = record.replaceAll("(WUB)+", " ").trim();
        System.out.println(record);
    }
}
```
