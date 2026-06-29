# Question 1859B - Olya and Game with Arrays

## Problem

You are given `n` arrays.

You may perform exactly one operation on every array:

* Choose one element from the array.
* Move it to any other array.

After all operations are performed, the **beauty** is defined as the sum of the minimum element of every array.

Find the **maximum possible beauty**.

---

## Initial Thought Process

* Since every array must send exactly one element away, removing its smallest element would increase its minimum to the second smallest.
* Therefore, for every array, only two values are important:

  * Smallest element.
  * Second smallest element.
* Initially, it seems that only the array containing the global minimum should contribute its minimum while every other array contributes its second minimum.
* However, this is not always optimal.

---

## Insight

* Every array except one will eventually contribute its **second smallest element** as its minimum.
* One array can receive the globally smallest element, allowing it to contribute that value instead.
* To maximize the total beauty:

  * Add the second smallest element from every array.
  * Replace the **smallest second minimum** with the **global minimum**.

Thus, only the minimum and second minimum of each array are ever needed.

---

### Algorithm

```text id="alg1859b"
READ n

sumSecond = 0
globalMin = INF
smallestSecond = INF

FOR each array:
    FIND smallest and second smallest element

    sumSecond += secondSmallest
    globalMin = min(globalMin, smallest)
    smallestSecond = min(smallestSecond, secondSmallest)

PRINT sumSecond - smallestSecond + globalMin
```

---

## Edge Cases

* Only one array.
* Arrays of size `2` (minimum possible size).
* Global minimum and smallest second minimum belong to different arrays.
* Duplicate minimum or second minimum values.
* Very large values (use `long` for the answer).

---

## Time and Space Complexity

* **Time Complexity:** `O(total elements)` - every element is visited exactly once.
* **Space Complexity:** `O(1)` - only a few variables are maintained while reading the input.

---

## Java Code

```java id="code1859b"
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        int t = Integer.parseInt(br.readLine());

        while (t-- > 0) {
            int n = Integer.parseInt(br.readLine());

            long sumSecond = 0;
            int globalMin = Integer.MAX_VALUE;
            int smallestSecond = Integer.MAX_VALUE;

            while (n-- > 0) {
                int m = Integer.parseInt(br.readLine());
                StringTokenizer st = new StringTokenizer(br.readLine());

                int min1 = Integer.MAX_VALUE;
                int min2 = Integer.MAX_VALUE;

                for (int i = 0; i < m; i++) {
                    int x = Integer.parseInt(st.nextToken());

                    if (x < min1) {
                        min2 = min1;
                        min1 = x;
                    } else if (x < min2) {
                        min2 = x;
                    }
                }

                sumSecond += min2;
                globalMin = Math.min(globalMin, min1);
                smallestSecond = Math.min(smallestSecond, min2);
            }

            System.out.println(sumSecond - smallestSecond + globalMin);
        }
    }
}
```
