# Question 59A - Word

## Problem

Given a string `s`, you need to convert it either entirely to uppercase or entirely to lowercase.

The rule is:

* If the string has **more uppercase letters**, convert the whole string to **uppercase**
* Otherwise (lowercase ≥ uppercase), convert it to **lowercase**

---

## Initial Thought Process

* We need to count how many characters are lowercase.
* Uppercase count can be derived from total length.
* Compare both counts.
* Apply transformation based on majority rule.

---

## Insight

* This is a **frequency comparison problem**.
* We only need one counter (lowercase is enough).
* Tie case (equal counts) goes to lowercase.
* No need for extra data structures.

---

## Algorithm

```text id="alg59a"
SET lowerCaseCount = 0

FOR each character c in message:
    IF c is lowercase:
        lowerCaseCount++

upperCaseCount = length - lowerCaseCount

IF lowerCaseCount < upperCaseCount:
    PRINT uppercase version of message
ELSE:
    PRINT lowercase version of message
```

---

## Edge Cases

* All lowercase → already lowercase output
* All uppercase → convert to uppercase
* Equal uppercase and lowercase → convert to lowercase
* Single character → unchanged logically

---

## Time and Space Complexity

* **Time Complexity:** `O(n)` — one pass through string
* **Space Complexity:** `O(1)` — only a counter used

---

## Java Code (Your Exact Approach)

```java id="code59a_user"
import java.io.*;

public class Main {
    public static void main(String [] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String message = br.readLine();
        int lowerCaseCount = 0;
        
        for (int i = 0; i < message.length(); i++) {
            if (97 <= message.charAt(i) && message.charAt(i) <= 122) {
                lowerCaseCount++;
            }
        }
        
        if (lowerCaseCount < (message.length() - lowerCaseCount)) {
            System.out.println(message.toUpperCase());
        }
        else {
            System.out.println(message.toLowerCase());
        }
    }
}
```
