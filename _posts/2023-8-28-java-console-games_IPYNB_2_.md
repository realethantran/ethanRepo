---
toc: True
comments: True
layout: post
title: Java Console Games
description: None
type: hacks
courses: {'csa': {'week': 1}}
---

## Thoughts

After thinking to myself and talking with my teammate, Tay, we found that it would be best to put each of the games in their own, individual classes. By doing this, it allows the games to be evaluated easier compared to the code provided in the blog, which when I look at it; appears all over the place.


```java
import java.util.Scanner;

public class TicTacToe { // Unit 5
    private String[] board = {"1", "2", "3", "4", "5", "6", "7", "8", "9"};
    private String currentPlayer = "X";
    private String player2 = "O";
    private int turn = 0;
    private boolean quit = false; // Unit 3
    private Scanner scanner = new Scanner(System.in);

    public void play() {
        System.out.println("Tic Tac Toe");
        System.out.println("Do you want to play against a friend or the computer?");
        System.out.println("Type 1 for friend, 2 for computer");
        int choice = scanner.nextInt();
        if (choice == 1) {
            System.out.println("Type the number of the square you want to place your piece in");
            while (!quit) {
                displayBoard();
                makeMove(currentPlayer);
                if (checkWin(currentPlayer)) {
                    System.out.println("Player " + currentPlayer + " wins!");
                    quit = true;
                } else if (turn == 9) {
                    System.out.println("It's a tie!");
                    quit = true;
                } else {
                    switchPlayer();
                }
            }
        } else if (choice == 2) {
            String computer = "O";
            System.out.println("Type the number of the square you want to place your piece in");
            while (!quit) {
                displayBoard();
                if (currentPlayer.equals("X")) {
                    makeMove(currentPlayer);
                    if (checkWin(currentPlayer)) {
                        System.out.println("Player " + currentPlayer + " wins!");
                        quit = true;
                    } else if (turn == 9) {
                        System.out.println("It's a tie!");
                        quit = true;
                    }
                    switchPlayer();
                } else {
                    makeComputerMove(computer);
                    if (checkWin(computer)) {
                        System.out.println("Computer wins!");
                        quit = true;
                    }
                    switchPlayer();
                }
            }
        }
        scanner.close();
    }

    private void displayBoard() {
        System.out.println(board[0] + " | " + board[1] + " | " + board[2]);
        System.out.println(board[3] + " | " + board[4] + " | " + board[5]);
        System.out.println(board[6] + " | " + board[7] + " | " + board[8]);
    }

    private void makeMove(String player) {
        System.out.println("Player " + player + "'s turn");
        int move = scanner.nextInt();
        if (move >= 1 && move <= 9 && board[move - 1].equals(String.valueOf(move))) {
            board[move - 1] = player;
            turn++;
        } else {
            System.out.println("Invalid move. Try again.");
        }
    }

    private void makeComputerMove(String computer) {
        int move;
        do {
            move = (int) (Math.random() * 9) + 1;
        } while (!board[move - 1].equals(String.valueOf(move)));
        board[move - 1] = computer;
        turn++;
    }

    private void switchPlayer() {
        if (currentPlayer.equals("X")) {
            currentPlayer = player2;
        } else {
            currentPlayer = "X";
        }
    }

    private boolean checkWin(String player) { 
        // Check for win conditions here (e.g., horizontal, vertical, diagonal)
        return false; // Unit 3
    }

    public static void main(String[] args) {
        TicTacToe game = new TicTacToe();
        game.play();
    }
}
TicTacToe.main(null)
```

    Tic Tac Toe
    Do you want to play against a friend or the computer?
    Type 1 for friend, 2 for computer
    Type the number of the square you want to place your piece in
    1 | 2 | 3
    4 | 5 | 6
    7 | 8 | 9
    Player X's turn
    1 | 2 | X
    4 | 5 | 6
    7 | 8 | 9
    Player O's turn
    1 | O | X
    4 | 5 | 6
    7 | 8 | 9
    Player X's turn
    X | O | X
    4 | 5 | 6
    7 | 8 | 9
    Player O's turn
    X | O | X
    O | 5 | 6
    7 | 8 | 9
    Player X's turn
    Invalid move. Try again.
    X | O | X
    O | 5 | 6
    7 | 8 | 9
    Player O's turn
    X | O | X
    O | 5 | O
    7 | 8 | 9
    Player X's turn
    X | O | X
    O | X | O
    7 | 8 | 9
    Player O's turn
    X | O | X
    O | X | O
    O | 8 | 9
    Player X's turn
    X | O | X
    O | X | O
    O | 8 | X
    Player O's turn
    Invalid move. Try again.
    X | O | X
    O | X | O
    O | 8 | X
    Player X's turn
    Invalid move. Try again.
    X | O | X
    O | X | O
    O | 8 | X
    Player O's turn
    Invalid move. Try again.
    X | O | X
    O | X | O
    O | 8 | X
    Player X's turn
    Invalid move. Try again.
    X | O | X
    O | X | O
    O | 8 | X
    Player O's turn
    Invalid move. Try again.
    X | O | X
    O | X | O
    O | 8 | X
    Player X's turn
    Invalid move. Try again.
    X | O | X
    O | X | O
    O | 8 | X
    Player O's turn
    Invalid move. Try again.
    X | O | X
    O | X | O
    O | 8 | X
    Player X's turn
    Invalid move. Try again.
    X | O | X
    O | X | O
    O | 8 | X
    Player O's turn
    Invalid move. Try again.
    X | O | X
    O | X | O
    O | 8 | X
    Player X's turn
    Invalid move. Try again.
    X | O | X
    O | X | O
    O | 8 | X
    Player O's turn
    Invalid move. Try again.
    X | O | X
    O | X | O
    O | 8 | X
    Player X's turn
    Invalid move. Try again.
    X | O | X
    O | X | O
    O | 8 | X
    Player O's turn
    Invalid move. Try again.
    X | O | X
    O | X | O
    O | 8 | X
    Player X's turn
    Invalid move. Try again.
    X | O | X
    O | X | O
    O | 8 | X
    Player O's turn
    Invalid move. Try again.
    X | O | X
    O | X | O
    O | 8 | X
    Player X's turn
    Invalid move. Try again.
    X | O | X
    O | X | O
    O | 8 | X
    Player O's turn
    Invalid move. Try again.
    X | O | X
    O | X | O
    O | 8 | X
    Player X's turn
    Invalid move. Try again.
    X | O | X
    O | X | O
    O | 8 | X
    Player O's turn
    Invalid move. Try again.
    X | O | X
    O | X | O
    O | 8 | X
    Player X's turn
    Invalid move. Try again.
    X | O | X
    O | X | O
    O | 8 | X
    Player O's turn
    Invalid move. Try again.
    X | O | X
    O | X | O
    O | 8 | X
    Player X's turn
    Invalid move. Try again.
    X | O | X
    O | X | O
    O | 8 | X
    Player O's turn
    Invalid move. Try again.
    X | O | X
    O | X | O
    O | 8 | X
    Player X's turn
    Invalid move. Try again.
    X | O | X
    O | X | O
    O | 8 | X
    Player O's turn
    Invalid move. Try again.
    X | O | X
    O | X | O
    O | 8 | X
    Player X's turn
    Invalid move. Try again.
    X | O | X
    O | X | O
    O | 8 | X
    Player O's turn
    Invalid move. Try again.
    X | O | X
    O | X | O
    O | 8 | X
    Player X's turn
    Invalid move. Try again.
    X | O | X
    O | X | O
    O | 8 | X
    Player O's turn
    Invalid move. Try again.
    X | O | X
    O | X | O
    O | 8 | X
    Player X's turn
    It's a tie!



```java
import java.util.Scanner;

public class RockPaperScissors { // Unit 5
    public void play() { 
        System.out.println("Rock Paper Scissors");
        System.out.println("Type 'r' for rock, 'p' for paper, or 's' for scissors");
        
        Scanner scRPS = new Scanner(System.in); // Unit 1
        String userChoice = scRPS.nextLine().toLowerCase();
        scRPS.close();
        
        int random = (int) (Math.random() * 3);
        
        if (userChoice.equals("r")) {
            if (random == 1) {
                System.out.println("You chose rock\nThe computer chose paper\nYou lose!");
            } else if (random == 2) {
                System.out.println("You chose rock\nThe computer chose scissors\nYou win!");
            } else {
                System.out.println("You chose rock\nThe computer chose rock\nIt's a tie!");
            }
        } else if (userChoice.equals("p")) {
            if (random == 1) {
                System.out.println("You chose paper\nThe computer chose paper\nIt's a tie!");
            } else if (random == 2) {
                System.out.println("You chose paper\nThe computer chose scissors\nYou lose!");
            } else {
                System.out.println("You chose paper\nThe computer chose rock\nYou win!");
            }
        } else if (userChoice.equals("s")) {
            if (random == 1) {
                System.out.println("You chose scissors\nThe computer chose paper\nYou win!");
            } else if (random == 2) {
                System.out.println("You chose scissors\nThe computer chose scissors\nIt's a tie!");
            } else {
                System.out.println("You chose scissors\nThe computer chose rock\nYou lose!");
            }
        } else {
            System.out.println("Invalid input. Please try again.");
        }
    }

    public static void main(String[] args) { // Unit 9
        RockPaperScissors game = new RockPaperScissors();
        game.play();
    }
}
RockPaperScissors.main(null)
```

    Rock Paper Scissors
    Type 'r' for rock, 'p' for paper, or 's' for scissors
    You chose rock
    The computer chose scissors
    You win!



```java
import java.util.Scanner;

public class HigherOrLowerGame { // Unit 5
    public void horl() { 
        System.out.println("Higher or Lower"); 
        System.out.println("You have three guesses to guess the number I am thinking of between 1-8.");
        System.out.println("If you guess the number correctly, you win!");
        Scanner scHL = new Scanner(System.in); // Unit 1
        int randomG = (int) (Math.random() * 8) + 1;
        int guess = scHL.nextInt();
        for (int i = 3; i > 0; i--) { // Unit 3
            if (guess == randomG) {
                System.out.println("You win!");
                break;
        } else if (guess > randomG) {
                System.out.println("The number is lower");
            } else if (guess < randomG) {
                System.out.println("The number is higher");
            }
            guess = scHL.nextInt();
        }
        System.out.println("Game over.");
        scHL.close();
    }

    public static void main(String[] args) { // Unit 9
        HigherOrLowerGame game = new HigherOrLowerGame();
        game.horl();
    }
}
HigherOrLowerGame.main(null) 
```

    Higher or Lower
    You have three guesses to guess the number I am thinking of between 1-8.
    If you guess the number correctly, you win!
    The number is higher
    The number is lower
    You win!
    Game over.


## Adding a new game

Now, I will add a color guessing game to the mix!


```java
import java.util.Scanner;

public class ColorGuessingGame { // Unit 5

    public static void main(String[] args) { // Unit 9
        Scanner scanner = new Scanner(System.in);

        // Array of color descriptions
        String[] colorDescriptions = {
            "The color of the ocean",
            "Ferrari",
            "The color of grass",
            "What do you get when you mix red and blue?",
            "The color of an orange"
        };

        // Array of answers
        String[] colorAnswers = {
            "blue",
            "red",
            "green",
            "purple",
            "orange"
        };

        int score = 0; // Player's score

        System.out.println("Guess the Color!");
        System.out.println("Guess the color based on the description.");

        // Loop through each color description and prompt the user for guesses
       for (int i = 0; i < colorDescriptions.length; i++) {
            System.out.println("\nDescription: " + colorDescriptions[i]);
            System.out.print("Your guess: ");
            String guess = scanner.nextLine().toLowerCase(); // Convert input to lowercase, preventing case mismatch

            if (guess.equals(colorAnswers[i])) { // Compare user guess to the correct answer
                System.out.println("Correct! You guessed the color.");
                score++; // Increase score if the answer is correct
            } else {
                System.out.println("Incorrect. The correct color is: " + colorAnswers[i]);
            }
        }

        // Display final score
        System.out.println("\nGame over! You had a final score of " + score + " out of " + colorDescriptions.length);
    }
}
ColorGuessingGame.main(null)
```

    Guess the Color!
    Guess the color based on the description.
    
    Description: The color of the ocean
    Your guess: Incorrect. The correct color is: blue
    
    Description: Ferrari
    Your guess: Correct! You guessed the color.
    
    Description: The color of grass
    Your guess: Correct! You guessed the color.
    
    Description: What do you get when you mix red and blue?
    Your guess: Correct! You guessed the color.
    
    Description: The color of an orange
    Your guess: Correct! You guessed the color.
    
    Game over! You had a final score of 4 out of 5



```java
import java.util.Scanner;

public class ConsoleGame { // Unit 5
    public static final String DEFAULT = "\u001B[0m"; 
    public static final String ANSI_BLUE = "\u001B[34m"; 

    public ConsoleGame() {
        Scanner sc = new Scanner(System.in);

        this.menuString();
        try {
            int choice = sc.nextInt();
            System.out.print(ANSI_BLUE + choice + ": " + DEFAULT);
            if (!this.action(choice)) {
                new ConsoleGame(); // Recursively create a new instance of ConsoleGame to display the menu again.
            }
        } catch (Exception e) {
            sc.nextLine(); // error: clear buffer
            System.out.println(ANSI_BLUE + e + ": Not a number, try again." + DEFAULT);
            new ConsoleGame(); // Recursively create a new instance of ConsoleGame to display the menu again.
        }
        
        sc.close();
    }

    public void menuString() {
        String menuText = ANSI_BLUE 
            + "+------------------------------------+\n"
            + "| 0 - Quit                           |\n"
            + "| 1 - Higher or Lower                |\n"
            + "| 2 - Tic Tac Toe                    |\n"
            + "| 3 - Rock Paper Scissors            |\n"
            + "| 4 - Color Guessing Game            |\n"
            + "+------------------------------------+\n" 
            + DEFAULT;
        System.out.println(menuText);
    }

    private boolean action(int selection) { 
        boolean quit = false; // Unit 3
        switch (selection) {
            case 0:
                System.out.print(ANSI_BLUE + "Goodbye, World!" + DEFAULT); 
                quit = true; 
                break;
            case 1:
                tloz();
                break; 
            case 2:
                horl();
                break;
            case 3:
                rps();
                break;
            case 4:
                cgg();
                break;
            default:
                System.out.print(ANSI_BLUE + "Unexpected choice, try again." + DEFAULT);
        }
        System.out.println(DEFAULT);
        return quit;
    }

    public void horl() {
        HigherOrLowerGame.main(null); 
    }

    public void tloz() {
        TicTacToe.main(null); 
    }

    // Assuming you have a rps() method or you can add it
    public void rps() {
        RockPaperScissors.main(null); 
    }
    public void cgg() {
        ColorGuessingGame.main(null);
    }
    public static void main(String[] args) { // Unit 9
        new ConsoleGame(); 
    }

}
ConsoleGame.main(null); 
```

    [34m+------------------------------------+
    | 0 - Quit                           |
    | 1 - Higher or Lower                |
    | 2 - Tic Tac Toe                    |
    | 3 - Rock Paper Scissors            |
    | 4 - Color Guessing Game            |
    +------------------------------------+
    [0m
    [34m4: [0mGuess the Color!
    Guess the color based on the description.
    
    Description: The color of the ocean
    Your guess: Incorrect. The correct color is: blue
    
    Description: Ferrari
    Your guess: Incorrect. The correct color is: red
    
    Description: The color of grass
    Your guess: Correct! You guessed the color.
    
    Description: What do you get when you mix red and blue?
    Your guess: Correct! You guessed the color.
    
    Description: The color of an orange
    Your guess: Correct! You guessed the color.
    
    Game over! You had a final score of 3 out of 5
    [0m
    [34m+------------------------------------+
    | 0 - Quit                           |
    | 1 - Higher or Lower                |
    | 2 - Tic Tac Toe                    |
    | 3 - Rock Paper Scissors            |
    | 4 - Color Guessing Game            |
    +------------------------------------+
    [0m
    [34m0: [0m[34mGoodbye, World![0m[0m

