# Question 1849B - Monsters

## Problem

Given `n` monsters with health values and a damage value `k`, determine the order in which the monsters die.

In each attack:

* The first alive monster receives `k` damage.
* If its health becomes `0` or less, it dies and is removed.
* Otherwise, it moves to the end of the queue.

Print the indices of the monsters in the order they die.

---

## Initial Thought Process

* A direct simulation would repeatedly damage monsters and rotate them in the queue.
* However, `n` and health values can be large, making simulation inefficient.
* Each attack reduces a monster's health by exactly `k`.
* Instead of tracking every attack, we should determine what characteristic decides when a monster finally dies.

---

## Insight

* Each attack reduces a monster's health by exactly `k`.
* Repeatedly subtracting `k` preserves the value of:`health % k`
* A monster eventually reaches its remainder before receiving the final killing blow.
* Monsters with larger remainders survive longer.
* If:

```text
health % k == 0
```

treat its remainder as `k`, since such monsters die after all monsters with remainders `1` to `k-1`.

Therefore:

* Compute the effective remainder for every monster.
* Sort by remainder in descending order.
* If remainders are equal, sort by original index in ascending order.

---

## Algorithm

```text
READ t

FOR each test case

    READ n, k

    CREATE list of (remainder, index)

    FOR i from 1 to n

        READ health

        remainder = health % k

        IF remainder == 0
            remainder = k

        STORE (remainder, i)

    SORT list by:
        larger remainder first
        smaller index first

    PRINT indices in sorted order
```

---

## Edge Cases

* Health exactly divisible by `k`

```text
health % k = 0
```

Treat remainder as `k`.

* Multiple monsters with the same remainder

```text
Sort by original index.
```

* Single monster

```text
Answer is simply index 1.
```

---

## Time and Space Complexity

* **Time Complexity:** `O(n log n)` due to sorting
* **Space Complexity:** `O(n)` for storing remainders and indices

---

## Java Code

```java
import java.io.*;
import java.util.*;

public class Main {

    static class Monster {
        long rem;
        int idx;

        Monster(long rem, int idx) {
            this.rem = rem;
            this.idx = idx;
        }
    }

    public static void main(String[] args) throws Exception {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        int t = Integer.parseInt(br.readLine());

        while (t-- > 0) {

            StringTokenizer st = new StringTokenizer(br.readLine());

            int n = Integer.parseInt(st.nextToken());
            long k = Long.parseLong(st.nextToken());

            st = new StringTokenizer(br.readLine());

            Monster[] monsters = new Monster[n];

            for (int i = 0; i < n; i++) {

                long health = Long.parseLong(st.nextToken());

                long rem = health % k;

                if (rem == 0) {
                    rem = k;
                }

                monsters[i] = new Monster(rem, i + 1);
            }

            Arrays.sort(monsters, (a, b) -> {
                if (a.rem != b.rem) {
                    return Long.compare(b.rem, a.rem);
                }
                return Integer.compare(a.idx, b.idx);
            });

            StringBuilder ans = new StringBuilder();

            for (Monster monster : monsters) {
                ans.append(monster.idx).append(" ");
            }

            System.out.println(ans);
        }
    }
}
```
