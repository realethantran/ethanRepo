---
toc: True
comments: True
layout: post
title: U4 | Iteration
description: while Loops, for Loops, Developing Algorithms Using Strings, Nested Iteration, Informal code analysis >>> AP Exam Weighting 17.5-22.5%
type: hacks
courses: {'csa': {'week': 8}}
authors: Aliya, Ekam, Emma, Raunak, Luna
---

# U4 | Iteration

---

# 4.1 while Loops

---

- A while loop is a fundamental control structure in programming used for repeated execution of a block of code as long as a condition is true.
- The loop starts by evaluating the condition. If the condition is true, the code inside the loop is executed.
- After each iteration, the condition is re-evaluated, and if it's still true, the loop continues.
If the condition is false initially, the loop code is never executed.
- While loops are used when you don't know in advance how many times the loop needs to execute.
- There's a risk of infinite loops if the condition never becomes false, so be cautious.
You can use variables and complex expressions as loop conditions.
- It's essential to update the loop control variable within the loop to prevent infinite loops.
- While loops are typically used for tasks such as iterating over collections or waiting for a specific condition to be met.
- You can always break out of a while loop prematurely using the break statement.

## Example of While Loops


```java
public class PyramidPattern {
    public static void main(String[] args) {
        int height = 5;
        int row = 1;

        while (row <= height) {
            int spaces = height - row;
            int stars = 2 * row - 1;

            // Print spaces
            int spaceCount = spaces;
            while (spaceCount > 0) {
                System.out.print(" ");
                spaceCount--;
            }

            // Print stars
            int starCount = stars;
            while (starCount > 0) {
                System.out.print("*");
                starCount--;
            }

            System.out.println(); // Move to the next line for the next row
            row++;
        }
    }
}
```

# 4.2 for Loops

---

- Iterative statement that checks for condition
- Repeatedly execute a a block of code as long as the condition is met
- Condition specifies amount of times

# for Loops vs. while Loops
- while Loops: use when number of iterations is unknown
- for Loops: use when number of iterations is known


```java
int i = 0;
while (i < 5) {
    System.out.println(i);
    i++;
}
```

    0
    1
    2
    3
    4



```java
for (int i = 0; i < 5; i++) {
    System.out.println(i);
}
```

    0
    1
    2
    3
    4


- Three parts in for loop header: variable initialization, Boolean (conditional) expression, and increment/decrement statement

Question: Which part is which?

- variable initialization (int i=0): sets variable before loop starts
- Boolean (conditional) expression (i < 5): defines condition for loop to run, in this case, the loop continues as long as i is less than 5, so loops 5 times i 05
- increment/decrement statement (i++): increases variable each time code block in the loop is executed, in this case it increases by 1
- variable can be used in the code block for other various reasons besides specifying how many times the loop will repeat
- Boolean (conditional) expression and increment/decrement statement together determine how many times the loop will repeat

Calculate and print the sum of all even numbers from 1 to a given positive integer ‘n’ (user input n)



```java
import java.util.Scanner;

public class EvenNumberSum {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Enter any positive integer 'n': ");
        int n = scanner.nextInt();

        if (n < 1) {
            System.out.println("Enter any positive integer 'n'");
        } else {
            int sum = 0;
            for (int i = 2; i <= n; i += 2) {
                sum += i;
            }

            System.out.println("Sum of even numbers from 1 to " + n + " equals: " + sum);
        }
    }
}
EvenNumberSum.main(null);
```

    Enter any positive integer 'n': Sum of even numbers from 1 to 12 equals: 42


# 4.3 Developing Algorithms Using Strings

---

LEARNING OBJECTIVES:
For algorithms in the context of a particular specification that involves ```String``` objects:
- identify standard algorithms
- modify standard algorithms
- develop an algorithm


**Java has many methods that are helpful when working with strings:**

* ```String .substring``` --> retrieves portion of a string
* ```String .equals``` --> compares two strings
* ```String .length``` --> returns length of a string
* ```for Loop``` --> iterating through characters of a string

<br>
<br>

<h3> Finding a substring within a string </h3>

We can use the "window" method:

A "window" is created the same length as the substring. We then iterate through the main string in sections and compare to the substring

For example:

<h3> I T E R A T E </h3>with substring "ERA"

<br>
<br>
<br>


```java
public class StringFinder {
    public static void main(String[] args) {
        String word = "iterate";
        String sub = "era";
        boolean found = false;

        // Adjusted loop range to prevent out-of-bounds error
        for (int i = 0; i <= word.length() - sub.length(); i++) {
            String portion = word.substring(i, i + sub.length()).toLowerCase(); // Convert to lowercase for case-insensitive comparison
            if (portion.equals(sub.toLowerCase())) {
                found = true;
                break; // Substring found, exit the loop early
            }
        }

        if (found)
            System.out.println("Substring is found within the string!");
        else
            System.out.println("Substring is NOT within the string");
    }
}
StringFinder.main(null);
```

    Substring is found within the string!


<h4> POPCORN HACK: Run the code.. what happened? How can we fix it?</h4>

Tell us below!

<br>
When the code cell is executed, an out of bounds error occurs. This is the case because there are no letters after the final letter even though the for loop continues until the end of the word. This can be corrected by changing the upper bound to i = word.duration() - sub.duration()
<br>


<h4> Another issue:</h4>

<h3> I T E R A T E </h3>
What if our substring was the word "RATE"? Note that RATE is at the end of the whole string

<br>
The provided code will correctly identify that the substring is within the word if the substring "RATE" is at the end of the word "iterate". 
<br>

<h3> HACKS </h3>

**Create a algorithm similar to the one above. Except this time, use iteration to count the number of vowels within the main string.**

HINT: Use the boolean expressions we have learned in previous lessons. Which would you use when comparing your "window" with multiple options of substrings?


```java
public class vowelCount {
    public static void main(String[] args) {
        String word = "hello";
        int vowelCount = 0; 

        for (int i = 0; i < word.length(); i++) {
            char currentChar = word.charAt(i);

            if (currentChar == 'a' || currentChar == 'e' || currentChar == 'i' || currentChar == 'o' || currentChar == 'u') {
                vowelCount++;
            }
        }

        System.out.println("Number of vowels in the string: " + vowelCount);
    }
}
vowelCount.main(null)
```

    Number of vowels in the string: 2


# 4.4 Nested Iteration

**nested iteration**
<details>occurs when we have a loop inside of another loop, similar to nested conditional statements in unit 3

When you have one loop inside another, the inner loop has to finish all its rounds before the outer loop moves to the next round. If the inner loop has a "stop" command, it only stops for that round of the outer loop. The next time the outer loop starts a new round, the inner loop starts over.

If you have two nested loops without stops, and the outer one runs n times while the inner one runs m times each time the outer one goes around, the inner loop will run m times n times, which is m * n times in total. This rule also applies if you have more than two nested loops. To find the total number of times the innermost loop runs, just multiply how many times each loop runs per round.


```java
public class NestedLoopsDemo {
    public static void main(String[] args) {
        int n = 3; //numb of times the outside loop runs
        int m = 2; //numb of times the inside loop runs

        //the nested loops
        for (int i = 1; i <= n; i++) {
            System.out.println("Outer loop iteration: " + i);
            for (int j = 1; j <= m; j++) {
                System.out.println("Inner loop iteration: " + j);
            }
        }
    }
}
NestedLoopsDemo.main(null)
```

    Outer loop iteration: 1
    Inner loop iteration: 1
    Inner loop iteration: 2
    Outer loop iteration: 2
    Inner loop iteration: 1
    Inner loop iteration: 2
    Outer loop iteration: 3
    Inner loop iteration: 1
    Inner loop iteration: 2


### Break Statement

**break statement**
<details>is used to exit a loop prematurely, typically when a certain condition is met. In the case of nested loops, it can be used to break out of the innermost loop.


```java
public class BreakExample {
    public static void main(String[] args) {
        for (int i = 1; i <= 3; i++) {
            System.out.println("Outer loop iteration " + i);

            for (int j = 1; j <= 3; j++) {
                System.out.println("Inner loop iteration " + j);

                if (i == 2 && j == 2) {
                    System.out.println("Breaking inner loop");
                    break; //break out of the inside loop when i is 2 and j is 2.
                }
            }
        }
    }
}
BreakExample.main(null)
```

    Outer loop iteration 1
    Inner loop iteration 1
    Inner loop iteration 2
    Inner loop iteration 3
    Outer loop iteration 2
    Inner loop iteration 1
    Inner loop iteration 2
    Breaking inner loop
    Outer loop iteration 3
    Inner loop iteration 1
    Inner loop iteration 2
    Inner loop iteration 3


### Popcorn HACK

When the targetNumber is found, you can print a message and use the break statement to exit the loop. When it's not found, you can print a message indicating that the number was not found.


```java
public class BreakHack {
    public static void main(String[] args) {
        int targetNumber = 42; // num we want
        int[] numbers = {10, 20, 30, 40, 50, 60, 70}; // array

        boolean found = false; // variable to track if the target number is found

        for (int number : numbers) {
            if (number == targetNumber) {
                found = true;
                System.out.println("Number " + targetNumber + " found.");
                break; 
            }
        }

        if (!found) {
            System.out.println("Number " + targetNumber + " was not found.");
        }
    }
}
BreakHack.main(null)
```

    Number 42 was not found.


### Continue Statement

**continue statement**
<details>is used to skip the current iteration of a loop and move to the next iteration. In the case of nested loops, it applies to the innermost loop.


```java
public class ContinueExample {
    public static void main(String[] args) {
        for (int i = 1; i <= 3; i++) {
            System.out.println("Outer loop iteration " + i);

            for (int j = 1; j <= 3; j++) {
                if (i == 2 && j == 2) {
                    System.out.println("Skipping inner loop iteration " + j);
                    continue; //skip the iteration when i is 2 and j is 2.
                }
                System.out.println("Inner loop iteration " + j);
            }
        }
    }
}
ContinueExample.main(null)
```

### Patterns and Shapes


```java
import java.util.Scanner;

public class InteractivePyramid {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Enter the symbol you want to use: ");
        char symbol = scanner.next().charAt(0);

        System.out.print("Enter the number of rows for the pyramid: ");
        int numRows = scanner.nextInt();

        for (int i = 1; i <= numRows; i++) {
            //print space before the symbol
            for (int j = 1; j <= numRows - i; j++) {
                System.out.print(" ");
            }

            //print
            for (int k = 1; k <= 2 * i - 1; k++) {
                System.out.print(symbol);
            }

            System.out.println(); //next line
        }
        scanner.close();
    }
}
InteractivePyramid.main(null)
```

    Enter the symbol you want to use: Enter the number of rows for the pyramid:        W
          WWW
         WWWWW
        WWWWWWW
       WWWWWWWWW
      WWWWWWWWWWW
     WWWWWWWWWWWWW
    WWWWWWWWWWWWWWW


## Hacks

1. **Modify pyramid code:**

- Create different patterns (other then pyramid) by modifying nested loop structure

### Inverted Pyramid


```java
import java.util.Scanner;

public class InvertPyramid {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Enter the symbol you want to use: ");
        char symbol = scanner.next().charAt(0);

        System.out.print("Enter the number of rows for the inverted pyramid: ");
        int numRows = scanner.nextInt();

        for (int i = numRows; i >= 1; i--) {
            // print spaces before the symbol
            for (int j = 1; j <= numRows - i; j++) {
                System.out.print(" ");
            }

            // print symbols
            for (int k = 1; k <= 2 * i - 1; k++) {
                System.out.print(symbol);
            }

            System.out.println(); // next line
        }
        scanner.close();
    }
}
InvertPyramid.main(null)
```

    Enter the symbol you want to use: Enter the number of rows for the inverted pyramid: WWWWWWWWWWWWWWW
     WWWWWWWWWWWWW
      WWWWWWWWWWW
       WWWWWWWWW
        WWWWWWW
         WWWWW
          WWW
           W


2. **Questions**

- What is a nested iteration, continue statement, and break statement (in your own words)?

A nested iteration is a series of loops nested inside one another. A continue statement instructs the loop to continue its execution. A break statement causes the code to break from the loop.

- Create a simple example of a continue statement **or** break statement

There is a list of basketball players. There is also a list of players who are ineligible to participate in the game for various reasons. To move to the next player on the roster instead of processing ineligible players inside the loop, I use a continue statement. 


```java
import java.util.ArrayList;
import java.util.List;

public class BasketballRoster {
    public static void main(String[] args) {
        List<String> playerRoster = new ArrayList<>();
        playerRoster.add("Player1");
        playerRoster.add("Player2");
        playerRoster.add("Player3");
        playerRoster.add("Player4");
        playerRoster.add("Player5");

        // Assume some players are ineligible for the game
        List<String> ineligiblePlayers = new ArrayList<>();
        ineligiblePlayers.add("Player2");
        ineligiblePlayers.add("Player4");

        System.out.println("Basketball Roster:");

        for (String player : playerRoster) {
            // Check if the player is ineligible
            if (ineligiblePlayers.contains(player)) {
                System.out.println(player + " is ineligible for the game. Skipping...");
                continue;  // Skip to the next iteration
            }

            // Process the eligible player
            System.out.println("Playing with " + player);
        }
    }
}
BasketballRoster.main(null)
```

    Basketball Roster:
    Playing with Player1
    Player2 is ineligible for the game. Skipping...
    Playing with Player3
    Player4 is ineligible for the game. Skipping...
    Playing with Player5


---

# 4.5 Informal Code Analysis

<b>Learning objective</b>: Compute statement execution counts & informal run-time comparison of iterative statements

<b>Essential Knowledge</b>: A statement execution count indicates the number of times a statement is executed by the program

<h3> What IS informal code analysis? </h3>

Answer: Computing informal runtime


```java
// CODE EXAMPLE #1 (for loop)
public class InformalCodeAnalysis {
    public static void main(String[] args) {
        int count = 0;
        for (int k = 0; k < 30; k++)
        {
            if (k % 3 == 0) // statement 1
            {
                count++; // statement 2
            }
        }
    }
}
```

<b>How many times will statement 1 execute? </b>

Answer: 10

<b>How many times will statement 2 execute?</b>

Answer: 30


```java
// CODE EXAMPLE #2 (for loop)
public class InformalCodeAnalysis {
    public static void main(String[] args) {
        int count = 0;
        for (int k = 4; k < 30; k+=3)
        {
            count++; // statement 3
        }
        System.out.println(count);
    }
}
InformalCodeAnalysis.main(null)
```

    9


<b>How many times will statement 3 execute?</b>

Answer: 9


```java
// Rewrite the code segment below to have a faster run-time based on statement execution counts
for (int k = 0; k < 135; k++)
{
    if (k % 5 == 0)
    {
        System.out.println(k);
    }
}

// Runs 27 times instead of 135 times
for (int k = 0; k < 135; k+=5)
{
    System.out.println(k);
}
```

    0
    5
    10
    15
    20
    25
    30
    35
    40
    45
    50
    55
    60
    65
    70
    75
    80
    85
    90
    95
    100
    105
    110
    115
    120
    125
    130
    0
    5
    10
    15
    20
    25
    30
    35
    40
    45
    50
    55
    60
    65
    70
    75
    80
    85
    90
    95
    100
    105
    110
    115
    120
    125
    130



```java
// CODE EXAMPLE #3 (while loop)

int num = (int)(Math.random() * 10);
while (num % 2 != 0)
{
    num = (int)(Math.random() * 10) // statement 4
}
```

<b>What is the min/max number of times statement 4 will execute?</b>

Answer: The minimum amount of time is 0 and the largest amount of time is infinite.


```java
// CODE EXAMPLE #4 (nested loop)

for (int outer = 0; outer < 3; outer++)
{
    for (int inner = 0; inner < 4; inner++)
    {
        // statement #5
    }
}
```

<b>How many times will statement #5 execute?</b>

Answer: 12 times


```java
// CODE EXAMPLE #5 (nested loop)

int k = 0;
while (k < 5)
{
    int x = (int)(Math.random() * 6) + 1;
    while (x != 6)
    {
        // statement #6
        x = (int)(Math.random() * 6) + 1;
        System.out.println(x);
    }
    k++;
}
```

    3
    1
    1
    6
    4
    3
    1
    6
    2
    1
    2
    2
    3
    5
    4
    5
    5
    2
    5
    2
    4
    1
    5
    6
    6
    2
    1
    5
    2
    1
    4
    5
    2
    3
    1
    2
    3
    5
    4
    6


<b>How many times will statement #6 execute?</b>

Answer: Between 0 and an infinite number of times.

# 4.5 Hacks


<b>#1 How many times will statement #1 and statement #2 execute in the code segments below? </b>

Statement 1: 1000 times

Statement 2: 44 times


```java
for (int k = 0; k < 1000; k++)
{
    // statement #1
}
```


```java
for (int k = 6; k < 50; k++)
{
    // statement #2
}
```

<b>#2 How many times will statement #3 execute for the code segment below?</b>

Statement 3: 28 times


```java
int k = 1;
while (k <=7)
{
    for (int z = 0; z < 4; z++)
    {
        // statement #3
    }
    k++;
}
```

<b>#3 Create 3 seperate code segments that execute a statement 10 times using: </b>

(a) a for loop

(b) a while loop

(c) a nested loop


```java
// 3a code
public class ThreeA {
    public static void main(String[] args) {
        for (int i = 0; i < 10; i++) {
            System.out.println((i + 1));
        }
    }
}
ThreeA.main(null)
```

    1
    2
    3
    4
    5
    6
    7
    8
    9
    10



```java
// 3b code
public class ThreeB {
    public static void main(String[] args) {
        int i = 0;
        while (i < 10) {
            System.out.println(i + 1);
            i++;
        }
    }
}
ThreeB.main(null)
```

    1
    2
    3
    4
    5
    6
    7
    8
    9
    10



```java
// 3c code
public class ThreeC {
    public static void main(String[] args) {
        for (int i = 0; i < 10; i++) {
            for (int j = 0; j < 1; j++) { // Inner loop only runs once
                System.out.println((i + 1) );
            }
        }
    }
}
ThreeC.main(null)
```

    1
    2
    3
    4
    5
    6
    7
    8
    9
    10

