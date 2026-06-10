# Question 282A - Bit++

## Problem

Given n operations, determine the final value after executing all operations starting from 0.

Each operation is either an increment or decrement operation:

* `++X` or `X++` → increase value by 1
* `--X` or `X--` → decrease value by 1

---

## Initial Thought Process

* Read each operation as a string
* Identify whether the operation is increment or decrement
* Use the middle character of the string to determine the operation type
* Update the value accordingly

---

## Insight

* All operations have a fixed format of length 3
* The middle character (`op[1]`) determines the operation:

  * `'+'` → increment
  * `'-'` → decrement
* No need to compare full strings

---

## Algorithm

```
INPUT n
SET value = 0

FOR i = 1 TO n
    READ operation

    IF operation[1] == '+'
        value = value + 1
    ELSE
        value = value - 1

PRINT value
```

---

## Edge Cases

* n = 1 → single operation
* All operations are increments → final value = n
* All operations are decrements → final value = -n
* Mixed operations → net sum of +1 and -1 operations

---

## Time and Space Complexity

* **Time Complexity:** `O(n)` where n is the number of operations
* **Space Complexity:** `O(1)` (only a single integer variable is used)

---

## Java Code

```java
import java.io.*;

public class Main {
    public static void main(String [] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int n = Integer.parseInt(br.readLine());
        int value = 0;
        
        for (int i = 0; i < n; i++){
            String op = br.readLine();
            
            if (op.charAt(1) == '+') {
                value++;
            }
            else {
                value--;
            }
        }
        
        System.out.println(value);
    }
}
```
