# Question 158A - Next Round

## Problem

Given **n participants** and their scores in a contest, determine how many participants advance to the next round.

A participant advances if:

* Their score is **greater than or equal to the score of the k-th participant**, and
* Their score is **strictly positive**

---

## Initial Thought Process

* Read `n` (number of participants) and `k` (position threshold)
* Store all participant scores in an array
* Identify the score of the k-th participant as the benchmark
* Iterate through all scores and count how many satisfy the advancement condition

---

## Insight

* Advancement is determined by a **threshold score**, not by relative position alone
* The k-th participant’s score defines the cutoff for qualification
* Only participants with **positive scores** are eligible, even if they meet the threshold condition
* There is no need to assume that the first `k` participants automatically qualify

---

## Algorithm

```
INPUT n, k
READ array arr of size n

SET threshold = arr[k - 1]
SET count = 0

FOR i = 1 TO n
    IF arr[i] >= threshold AND arr[i] > 0
        count = count + 1

PRINT count
```

---

## Edge Cases

* All scores are 0 → output = 0
* All scores are equal and positive → output = n
* k = 1 → threshold is the maximum score
* k = n → only participants with score ≥ last score and > 0 are counted
* Multiple participants tied at k-th score → all such participants may qualify

---

## Time and Space Complexity

* **Time Complexity:** `O(n)` — single pass through all scores
* **Space Complexity:** `O(n)` — storage for participant scores

---

## Java Code

```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws Exception {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        StringTokenizer st = new StringTokenizer(br.readLine());
        int n = Integer.parseInt(st.nextToken());
        int k = Integer.parseInt(st.nextToken());

        int[] arr = new int[n];

        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < n; i++) {
            arr[i] = Integer.parseInt(st.nextToken());
        }

        int threshold = arr[k - 1];
        int count = 0;

        for (int i = 0; i < n; i++) {
            if (arr[i] >= threshold && arr[i] > 0) {
                count++;
            }
        }

        System.out.println(count);
    }
}
```
