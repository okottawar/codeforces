# Question 110A - Nearly Lucky Number

## Problem

Given a number, determine whether it is **nearly lucky**.

A number is considered nearly lucky if:

* Count the number of digits that are either **4** or **7**
* If this count itself is a **lucky number** (contains only digits 4 and 7), print **"YES"**
* Otherwise, print **"NO"**

---

## Initial Thought Process

* Read the input number as a string
* Traverse each digit and count how many are `4` or `7`
* Convert the count into a string
* Check whether every digit of this count is either `4` or `7`
* Print `"YES"` if it is lucky; otherwise print `"NO"`

---

## Insight

* The original number does **not** need to consist only of lucky digits.
* Only the **count** of lucky digits matters.
* After counting, the problem reduces to checking whether the count is a lucky number.
* Using a string makes digit-by-digit traversal straightforward.

---

## Algorithm

```
INPUT number

SET count = 0

FOR each digit in number
    IF digit is '4' OR digit is '7'
        count = count + 1

CONVERT count to string

FOR each digit in count string
    IF digit is not '4' AND digit is not '7'
        PRINT "NO"
        EXIT

PRINT "YES"
```

---

## Edge Cases

* No lucky digits → count = 0 → output = NO
* Count = 4 → output = YES
* Count = 7 → output = YES
* Count = 44 or 77 → output = YES
* Count = 1, 2, 3, 5, 6, etc. → output = NO
* Input number itself may contain digits other than 4 and 7

---

## Time and Space Complexity

* **Time Complexity:** `O(n)` — one pass to count lucky digits and another pass over the digits of the count (at most a few digits)
* **Space Complexity:** `O(1)` — only a few variables are used

---

## Java Code

```java
import java.io.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String number = br.readLine();
        
        int count = 0;
        for (int i = 0; i < number.length(); i++) {
            char c = number.charAt(i);
            if (c == '4' || c == '7') {
                count++;
            }
        }

        String cnt = String.valueOf(count);
        for (int i = 0; i < cnt.length(); i++) {
            char c = cnt.charAt(i);
            if (c != '4' && c != '7') {
                System.out.println("NO");
                return;
            }
        }

        System.out.println("YES");
    }
}
```
