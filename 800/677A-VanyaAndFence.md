# Question 677A - Vanya and Fence

## Problem

Vanya and his **N** friends need to walk through a fence of height **H**.

Each friend's height is given:

* If a friend's height is **greater than H**, they must bend, occupying a width of **2**.
* Otherwise, they occupy a width of **1**.

Find the **minimum total width** required for everyone to pass through the fence.

---

## Initial Thought Process

* Every person contributes at least **1** unit of width.
* Taller people require an extra unit because they need to bend.
* Simply process each height and add the appropriate width.

---

## Insight

* Traverse the list of heights once.
* For each person:
  * If `height > H`, add **2** to the total width.
  * Otherwise, add **1**.
* The accumulated width is the answer.

---

## Algorithm

```
READ N and H

width = 0

FOR each person's height
    IF height > H
        width += 2
    ELSE
        width += 1

PRINT width
```

---

## Edge Cases

* All heights ≤ H → Total width = N
* All heights > H → Total width = 2 × N
* Mixed heights → Sum according to each person's contribution
* N = 1:
  * Height ≤ H → Width = 1
  * Height > H → Width = 2

---

## Time and Space Complexity

* **Time Complexity:** `O(n)`
* **Space Complexity:** `O(1)`

---

## Java Code

```java
import java.io.*;
import java.util.StringTokenizer;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        StringTokenizer st = new StringTokenizer(br.readLine());
        int n = Integer.parseInt(st.nextToken());
        int h = Integer.parseInt(st.nextToken());

        st = new StringTokenizer(br.readLine());
        int width = 0;

        for (int i = 0; i < n; i++) {
            int height = Integer.parseInt(st.nextToken());

            if (height > h) {
                width += 2;
            } else {
                width++;
            }
        }

        System.out.println(width);
    }
}
```
