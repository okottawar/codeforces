# Question 499B - Lecture

## Problem

A lecture is given using words from the first language.

You are given `m` pairs of words:

* The first word belongs to the original language.
* The second word is its synonym.

For every word in the lecture, print whichever of the two words has the **smaller length**.

If both words have the same length, print the **original word**.

---

## Initial Thought Process

* Each lecture word always belongs to the first language.
* We need to quickly determine whether to print the original word or its synonym.
* Since every original word has exactly one corresponding synonym, a hash map provides constant-time lookup.

---

## Insight

* We do not need to store both languages separately.
* While reading each pair, immediately determine the shorter word.
* Store a mapping: `originalWord → shorterWord`


where:

* If `original.length() <= synonym.length()`, map to the original word.
* Otherwise, map to the synonym.

Then, while reading the lecture, simply print the mapped value for each word.

---

### Algorithm

```text id="alg499b"
INITIALIZE HashMap<String, String> map

FOR each pair (original, synonym):

    IF original.length <= synonym.length:
        map[original] = original
    ELSE:
        map[original] = synonym

READ lecture words

FOR each lecture word:
    PRINT map[word]
```

---

## Edge Cases

* Original word is shorter → print the original word.
* Synonym is shorter → print the synonym.
* Both words have equal length → print the original word.
* Every lecture word is guaranteed to exist in the dictionary, so every lookup succeeds.

---

## Time and Space Complexity

* **Time Complexity:** `O(m + n)` - one pass to build the map and one pass through the lecture.
* **Space Complexity:** `O(m)` - hash map stores one entry for each dictionary pair.

---

## Java Code

```java id="code499b"
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        int n = Integer.parseInt(st.nextToken());
        int m = Integer.parseInt(st.nextToken());

        HashMap<String, String> map = new HashMap<>();
        for (int i = 0; i < m; i++) {
            st = new StringTokenizer(br.readLine());
            String original = st.nextToken();
            String synonym = st.nextToken();

            if (original.length() <= synonym.length())
                map.put(original, original);
            else
                map.put(original, synonym);
        }

        st = new StringTokenizer(br.readLine());
        while (n-- > 0) {
            System.out.print(map.get(st.nextToken()) + " ");
        }
    }
}
```
