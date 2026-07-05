# Question 580A - Kefa and First Steps

## Problem

Given a sequence of `n` integers, find the length of the **longest non-decreasing contiguous segment**.

A segment is non-decreasing if every element is **greater than or equal to** the previous element.

---

## Initial Thought Process

* Read `n` and the array of integers
* Traverse the array from left to right
* Keep track of the current non-decreasing segment length
* If the current element is greater than or equal to the previous one, extend the segment
* Otherwise, start a new segment
* Maintain the maximum segment length encountered

---

## Insight

* The problem only requires **contiguous** segments, so sorting is not allowed.
* At every index, we only need to compare the current element with the previous one.
* A single pass through the array is sufficient.

---

## Algorithm

```
INPUT n
READ array arr of size n

SET currentLength = 1
SET maxLength = 1

FOR i = 1 TO n - 1
    IF arr[i] >= arr[i - 1]
        currentLength = currentLength + 1
    ELSE
        currentLength = 1

    maxLength = maximum(maxLength, currentLength)

PRINT maxLength
```

---

## Edge Cases

* n = 1 → answer is 1
* Entire array is non-decreasing → answer is n
* Entire array is strictly decreasing → answer is 1
* All elements are equal → answer is n

---

## Time and Space Complexity

* **Time Complexity:** `O(n)` - single traversal of the array
* **Space Complexity:** `O(n)` - storage for the input array

---

## Java Code

```java
import java.io.*;
import java.util.StringTokenizer; 

public class Main {
    public static void main (String [] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int n = Integer.parseInt(br.readLine());
        StringTokenizer st = new StringTokenizer(br.readLine());
        int[] arr = new int[n];
        for(int i = 0; i < n; i++) {
            arr[i] = Integer.parseInt(st.nextToken());
        }
        
        int currLen = 1;
        int maxLen = 1;
        for (int i = 0; i < n-1; i++) {
            if (arr[i] <= arr[i+1]) currLen += 1;
            else currLen = 1;
            maxLen = Math.max(maxLen, currLen);
        }
        System.out.println(maxLen);
    }
}
```

