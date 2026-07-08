# Question 734A - Anton and Danik

## Problem

Anton and Danik played **N** games of chess.

A string of length **N** is given where:

* `'A'` means Anton won that game.
* `'D'` means Danik won that game.

Determine who won more games.

Print:

* `"Anton"` if Anton has more wins.
* `"Danik"` if Danik has more wins.
* `"Friendship"` if both have the same number of wins.

---

## Initial Thought Process

* Count the number of wins for each player.
* Instead of maintaining two separate counters, use a single score:
  * Increase it for Anton's wins.
  * Decrease it for Danik's wins.
* The final score directly determines the winner.

---

## Insight

* Every `'A'` contributes **+1**.
* Every `'D'` contributes **-1**.
* After traversing the entire string:
  * Positive score → Anton wins.
  * Negative score → Danik wins.
  * Zero → Equal wins (Friendship).

---

## Algorithm

```
READ N
READ games

score = 0

FOR each character in games
    IF character == 'A'
        score++
    ELSE
        score--

IF score > 0
    PRINT "Anton"
ELSE IF score < 0
    PRINT "Danik"
ELSE
    PRINT "Friendship"
```

---

## Edge Cases

* All games won by Anton → Anton
* All games won by Danik → Danik
* Equal number of wins → Friendship
* N = 1:
  * `"A"` → Anton
  * `"D"` → Danik

---

## Time and Space Complexity

* **Time Complexity:** `O(n)`
* **Space Complexity:** `O(1)`

---

## Java Code

```java
import java.io.*;

public class Main {
    public static void main (String [] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int n = Integer.parseInt(br.readLine());
        String games = br.readLine();

        int score = 0;

        for (int i = 0; i < n; i++) {
            if (games.charAt(i) == 'A') {
                score++;
            } else if (games.charAt(i) == 'D') {
                score--;
            }
        }

        if (score > 0)
            System.out.println("Anton");
        else if (score < 0)
            System.out.println("Danik");
        else
            System.out.println("Friendship");
    }
}
```
