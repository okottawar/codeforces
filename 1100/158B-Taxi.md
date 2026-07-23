# Codeforces 158B - Taxi

## Problem

Given:

* `n` groups of children.
* Each group has size `1`, `2`, `3`, or `4`.
* Every taxi can carry at most `4` children.
* Groups cannot be split across multiple taxis.

Find the **minimum number of taxis** required to transport all groups.

---

## Initial Thought Process

* Since group sizes are limited to only four possible values, counting each size is enough.
* Large groups should be placed first because they have fewer pairing options.
* Greedily pair groups that perfectly complement each other to maximize taxi utilization.

---

## Insight

* Count how many groups of each size exist.
* Every group of size `4` occupies an entire taxi.
* Every group of size `3` should be paired with one group of size `1` whenever possible.
* Pair groups of size `2` together.
* If one group of size `2` remains, it can share a taxi with up to two groups of size `1`.
* Any remaining groups of size `1` are packed four per taxi.

This greedy strategy always minimizes the number of taxis because larger groups have the fewest possible pairing choices.

---

## Algorithm

```text id="alg158b"
READ n

COUNT groups of sizes 1, 2, 3, and 4

taxis = count[4]

taxis += count[3]
REMOVE one size-1 group for each size-3 group if available

taxis += count[2] / 2

IF one size-2 group remains
    taxis++
    REMOVE up to two size-1 groups

ADD enough taxis for remaining size-1 groups
    (count[1] + 3) / 4

PRINT taxis
```

---

## Edge Cases

* All groups are of size `4` → each group needs its own taxi.
* All groups are of size `1` → four groups fit in one taxi.
* More size `3` groups than size `1` groups → some size `3` groups travel alone.
* An odd number of size `2` groups → the last one may share with up to two size `1` groups.
* Remaining size `1` groups fewer than `4` → they still require one taxi.

---

## Time and Space Complexity

* **Time Complexity:** `O(n)` — each group is processed exactly once.
* **Space Complexity:** `O(1)` — only four counters are maintained.

---

## Java Code

```java id="code158b"
import java.io.*;
import java.util.StringTokenizer;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int n = Integer.parseInt(br.readLine());
        int[] cnt = new int[5];
        StringTokenizer st = new StringTokenizer(br.readLine());
        for (int i = 0; i < n; i++) {
            cnt[Integer.parseInt(st.nextToken())]++;
        }
        int taxis = cnt[4];
        taxis += cnt[3];
        cnt[1] = Math.max(0, cnt[1] - cnt[3]);
        taxis += cnt[2] / 2;
        if (cnt[2] % 2 == 1) {
            taxis++;
            cnt[1] = Math.max(0, cnt[1] - 2);
        }
        taxis += (cnt[1] + 3) / 4;
        System.out.println(taxis);
    }
}
```
