---

---

- What is a boolean? 

A boolean expression represents  true (1) or false (0). Boolean is used as a conditional. 

- What values can a boolean represent? How many? 

Two values, true (1) and false (0).

- What is an example of when we’d use a boolean? 

An example of when to use boolean is when determining if a light is on (true) or off (false).

# Challenge Problem

Identify the issue(s) in the code below (hint: try running it yourself). Then, make the necessary corrections to ensure that the program runs as intended.

If you run the code and type in any answer, including the correct one, it returns false.


```Java
import java.util.Scanner;

public class Challenge {

    private static boolean isName = false;
    private static String name = "John";

    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);

        System.out.println("Guess my name!");

        String guess = sc.nextLine();
        System.out.println("Your guess: " + guess);

        if (guess.equals(name)) {
            isName = true;
        } else {
            System.out.println("Wrong! L Cope");
        }

        System.out.println(isName);
    }
}

Challenge.main(null);
```

    Guess my name!
    Your guess: John
    true


# Your Homework

Now that you know what boolean expressions are and how to write them, as well as several comparison methods, your task is to write a class that uses either the compareTo or comparator and compare. Then create two instances of these classes and demonstrate using if statements. 


```Java
class NBAPlayer implements Comparable<NBAPlayer> {
    private String name;
    private int pointsPerGame;

    public NBAPlayer(String name, int pointsPerGame) {
        this.name = name;
        this.pointsPerGame = pointsPerGame;
    }

    @Override
    public int compareTo(NBAPlayer otherPlayer) {
        return Integer.compare(this.pointsPerGame, otherPlayer.pointsPerGame);
    }

    public String getName() {
        return name;
    }

    public int getPointsPerGame() {
        return pointsPerGame;
    }
}

public class Main {
    public static void main(String[] args) {
        NBAPlayer jaMorant = new NBAPlayer("Ja Morant", 26);
        NBAPlayer lameloBall = new NBAPlayer("Lamelo Ball", 23);

        int comparisonResult = jaMorant.compareTo(lameloBall);

        if (comparisonResult < 0) {
            System.out.println(jaMorant.getName() + " has fewer points per game than " + lameloBall.getName());
        } else if (comparisonResult > 0) {
            System.out.println(jaMorant.getName() + " has more points per game than " + lameloBall.getName());
        } else {
            System.out.println(jaMorant.getName() + " and " + lameloBall.getName() + " have the same points per game.");
        }
    }
}
Main.main(null);
```

    Ja Morant has more points per game than Lamelo Ball


## BONUS: Create a program that checks if a year is a leap year or not.

Here is how the method should work: 

(1) Prompt the user to input any year that they would like <br>
(2) Determine if the year is a leap year or not <br>
(3) Print the necessary dialogue (ex. [year] is/is not a leap year) AND return the value of any boolean(s) used


```Java
import java.util.Scanner;

public class LeapYear {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter a year: ");
        int yearInput = scanner.nextInt();
        scanner.close();

        boolean isLeapYear = isLeapYear(yearInput);

        System.out.println(yearInput + (isLeapYear ? " is" : " is not") + " a leap year.");

        System.out.println("Is it a leap year? " + isLeapYear);
    }

    public static boolean isLeapYear(int year) {
        return (year % 4 == 0 && year % 100 != 0) || (year % 400 == 0);
    }
}
LeapYear.main(null);
```

    Enter a year: 2024 is a leap year.
    Is it a leap year? true


# Weird questions
1. !(true)&&(false) = ? what in boolean values?

!true (negation of true) = false. false && false = false. Thus, !(true) && (false) = false.

2. not ((((true and not (false)) ^ false) ^ true) && false) (remember PEMDASNAO!)

not (false) = true. true and true evaluates = true. (true ^ false) (XOR) = true. (true ^ true) (XOR) = false. (false && false) = false.
Thus, not ((((true and not (false)) ^ false) ^ true) && false) = not false = true.

3. 420 && 66 (Hint, convert to binary, then perform the operation)

420 = 110100100 in binary and 66 in binary = 1000010.

Thus, 420 && 66 = 000000000 = 0.

   1. If you got this one, try 89 OR 42

89 = 1011001 in binary and  42 in binary = 101010.

Thus, 89 OR 42 = 1111011 = 123.

