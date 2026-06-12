# Question 791A - Bear and Big Brother

## Problem

Given the weights of Limak and Bob, determine the number of years required for Limak's weight to become strictly greater than Bob's weight.

Each year:

* Limak's weight triples.
* Bob's weight doubles.

---

## Initial Thought Process

* The weight changes happen year by year.
* Since the growth rates are fixed, we can directly simulate each year.
* Continue updating both weights until Limak becomes heavier than Bob.
* Count the number of iterations performed.

---

## Insight

* The constraints are very small, so there is no need for any mathematical formula.
* A simple simulation exactly matches the process described in the problem statement.
* Each iteration represents one year.

---

### Algorithm

```text id="alg791a"
READ limak, bob

SET years = 0

WHILE limak <= bob
    limak = limak * 3
    bob = bob * 2
    years++

PRINT years
```

---

## Edge Cases

* Limak is already heavier than Bob → answer is `0`.
* Limak and Bob start with the same weight → at least one year is needed.
* Very small starting weights → simulation still terminates quickly.

---

## Time and Space Complexity

* **Time Complexity:** `O(years)` - One iteration is performed per year until Limak becomes heavier.

* **Space Complexity:** `O(1)` - Only a few integer variables are used.

---

## Java Code

```java id="code791a"
import java.io.*;
import java.util.StringTokenizer;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        int limak = Integer.parseInt(st.nextToken());
        int bob = Integer.parseInt(st.nextToken());

        int years = 0;

        while (limak <= bob) {
            limak *= 3;
            bob *= 2;
            years++;
        }

        System.out.println(years);
    }
}
```
