# Question 71A - Way Too Long Words

## Problem

Given N words, if the length of a word is **strictly greater than 10**, convert it into the format:

`first-character + (length - 2) + last-character`

Otherwise, print the word as it is.

---

## Initial Thought Process

* Read input words one by one
* If word length > 10, compress it using the required format
* Use `StringBuilder` to efficiently build the output
* Avoid storing all words in a data structure

---

## Insight

* Only words with length > 10 need transformation
* Middle characters are replaced by their count (`length - 2`)
* Output can be built incrementally using `StringBuilder` for efficiency
* No need for arrays or extra storage since processing is sequential

---

## Algorithm

```
CREATE STRINGBUILDER sb

FOR i = 1 TO N
    READ word

    IF length(word) > 10
        APPEND first_character
        APPEND (length - 2)
        APPEND last_character
    ELSE
        APPEND word

    APPEND newline

PRINT sb
```

---

## Edge Cases

* Word length = 1 → print as it is
* Word length = 10 → print as it is (boundary condition)
* Word length = 11 → compressed format applies
* All words short → no transformation needed
* All words long → all compressed

---

## Time and Space Complexity

* **Time Complexity:** `O(N)` where N = number of words
* **Space Complexity:** `O(1)` extra space (excluding output storage)

---

## Java Code

```java
import java.io.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        int n = Integer.parseInt(br.readLine());

        StringBuilder sb = new StringBuilder();

        for (int i = 0; i < n; i++) {
            String text = br.readLine();

            if (text.length() > 10) {
                sb.append(text.charAt(0));
                sb.append(text.length() - 2);
                sb.append(text.charAt(text.length() - 1));
            } else {
                sb.append(text);
            }

            sb.append("\n");
        }

        System.out.print(sb.toString());
    }
}
```
