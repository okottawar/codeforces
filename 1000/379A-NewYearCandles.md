# Question 379A - New Year Candles

## Problem

Given:

* `a` candles initially
* Every burned candle leaves behind one butt
* `b` butts can be exchanged for one new candle

Find the maximum number of candles that can be burned in total.

Example:

* `4 2` → `7`
* `5 3` → `7`

---

## Initial Thought Process

* We start by burning all `a` candles.
* This gives us `a` butts.
* Those butts can be exchanged for new candles.
* The newly obtained candles also produce more butts when burned.
* Therefore, the exchange process can repeat multiple times.

---

## Insight

* We only need to track:
  * Total candles burned
  * Current number of available butts
* As long as we have at least `b` butts, we can perform another exchange.
* Each exchange produces:

  * New candles = `butts / b`
  * Remaining butts = `butts % b`
* After burning the new candles, they create additional butts.

---

### Algorithm

```text id="alg379a"
INITIALIZE total = a
INITIALIZE butts = a

WHILE butts >= b:

    newCandles = butts / b

    total += newCandles

    butts = newCandles + (butts % b)

PRINT total
```

---

## Edge Cases

* `a < b` - No exchanges possible
* `a == b` - Exactly one exchange can be made
* Multiple rounds of exchanges - Continue until fewer than `b` butts remain

---

## Time and Space Complexity

* **Time Complexity:** `O(log a)` - number of exchange rounds
* **Space Complexity:** `O(1)` - only a few integer variables are used

---

## Java Code

```java id="code379a"
import java.io.*;
import java.util.StringTokenizer;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        StringTokenizer st = new StringTokenizer(br.readLine());

        int a = Integer.parseInt(st.nextToken());
        int b = Integer.parseInt(st.nextToken());

        int total = a;
        int butts = a;

        while (butts >= b) {
            int newCandles = butts / b;
            total += newCandles;
            butts = newCandles + (butts % b);
        }

        System.out.println(total);
    }
}
```
