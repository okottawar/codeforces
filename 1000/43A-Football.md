# Question 43A - Football

## Problem

A football match is played between exactly **two teams**.
You are given `n` goals, each written as the name of the team that scored that goal.

Your task is to determine which team scored more goals.

It is guaranteed that there are exactly **two distinct team names** in the input.

---

## Initial Thought Process

* Each goal contributes to one of the two teams.
* We need to count how many times each team appears.
* The team with the higher count is the winner.

---

## Insight

* Only **two unique teams** exist in the input.
* The first team we see can be treated as `team1`.
* Every other team name must belong to `team2`.
* No need for a hashmap since the number of teams is fixed.

---

## Key Idea

* Store the first team name as reference.
* Maintain two counters:

  * `score1` for first team
  * `score2` for second team (discovered on the fly)

---

## Algorithm

```text id="alg43a"
read n
read first team → team1
score1 = 1
score2 = 0

FOR remaining n-1 lines:
    read team

    IF team == team1:
        score1++
    ELSE:
        score2++

IF score1 > score2:
    PRINT team1
ELSE:
    PRINT team2
```

---

## Edge Cases

* First occurrence determines `team1`
* `team2` is discovered during processing
* Guaranteed exactly two teams → no extra validation needed

---

## Time and Space Complexity

* **Time Complexity:** `O(n)`
* **Space Complexity:** `O(1)` (no hashmap needed)

---

## Java Code

```java id="code43a"
import java.io.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        int n = Integer.parseInt(br.readLine());

        String team1 = br.readLine();
        int score1 = 1;
        String team2 = "";
        int score2 = 0;

        for (int i = 1; i < n; i++) {
            String team = br.readLine();

            if (team.equals(team1)) {
                score1++;
            } else {
                team2 = team;
                score2++;
            }
        }

        if (score1 > score2) {
            System.out.println(team1);
        } else {
            System.out.println(team2);
        }
    }
}
```
