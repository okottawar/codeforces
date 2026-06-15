# Question 230A - Dragons

## Problem

Kirito starts with strength `s`.

Each dragon has:

* Strength `x`
* Bonus `y`

Kirito can defeat a dragon only if his strength is **strictly greater** than the dragon's strength.

After defeating it:

```text id="dragon-bonus"
strength += bonus
```

Determine whether Kirito can defeat all dragons.

---

## Initial Thought Process

* Input order is not necessarily optimal.
* The statement allows fighting dragons in **any order**.
* We should fight easier dragons first to gain strength.

---

## Insight

* This is a **greedy + sorting** problem.
* Sort dragons by strength in ascending order.
* If Kirito cannot defeat the weakest remaining dragon, the answer is `"NO"`.

---

### Algorithm

```text id="alg230a"
STORE all dragons

SORT dragons by strength

FOR each dragon:
    IF strength <= dragonStrength:
        PRINT "NO"
        STOP

    strength += bonus

PRINT "YES"
```

---

## Edge Cases

* `strength == dragonStrength` → NO
* Only one dragon
* Initial strength smaller than the weakest dragon

---

## Time and Space Complexity

* **Time Complexity:** `O(n log n)` — sorting dominates
* **Space Complexity:** `O(n)` — storing dragons

---

## Java Code (Optimal Pattern)

```java id="code230a"
import java.io.*;
import java.util.StringTokenizer;

public class Main {
    public static void main(String [] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        int playerStrength = Integer.parseInt(st.nextToken());
        int numDragons = Integer.parseInt(st.nextToken());
        
        for (int i = 0; i < n; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            int dragonStrength = Integer.parseInt(st.nextToken());
            int bonus = Integer.parseInt(st.nextToken());
            
            if (playerStrength < dragonStrength) {
                System.out.println("NO");
                return;
            }
            
            playerStrength -= dragonStrength;
            playerStrength += bonus;
        }
    }
}
```
