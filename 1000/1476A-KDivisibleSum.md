# Question 1476A - K-divisible Sum

## Problem

You are given two integers `n` and `k`.

Find the minimum possible maximum value of an array of size `n` such that the sum of all elements is divisible by `k`.

Print the minimum value.

---

## Initial Thought Process

* The smallest possible sum of `n` positive integers is `n`.

* We need the smallest sum that is divisible by `k`.

* If `n` is already divisible by `k`, use `n`.

* Otherwise, move to the next multiple of `k`.

* The answer is the ceiling of: `valid sum / n`


---

## Insight

* We only need to find the smallest valid total sum.

* The smallest multiple of `k` greater than or equal to `n` is: `((n / k) + 1) * k`

* After finding this sum, distribute it among `n` elements.

* The minimum maximum element is: `ceil(sum / n)`


---

### Algorithm

```text id="alg1476a"
READ number of test cases

FOR each test case:
    READ n and k

    IF n is divisible by k:
        sum = n
    ELSE:
        sum = next multiple of k

    answer = ceil(sum / n)

    PRINT answer
```

---

## Edge Cases

* `n` is already divisible by `k` - answer is `1`.

* `k` is greater than `n` - the sum becomes `k`.

* `n` is just below a multiple of `k` - move to the next multiple.

---

## Time and Space Complexity

* **Time Complexity:** `O(t)` - each test case is processed once.
* **Space Complexity:** `O(1)` - only variables are used.

---

## Java Code

```java id="code1476a"
import java.io.*;
import java.util.StringTokenizer;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int t = Integer.parseInt(br.readLine());

        while (t-- > 0) {
            StringTokenizer st = new StringTokenizer(br.readLine());

            long n = Long.parseLong(st.nextToken());
            long k = Long.parseLong(st.nextToken());
            long sum;

            if (n % k == 0) {
                sum = n;
            } else {
                sum = ((n / k) + 1) * k;
            }
            long ans = (sum + n - 1) / n;

            System.out.println(ans);
        }
    }
}
```
