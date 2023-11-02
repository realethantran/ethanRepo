---
toc: True
comments: True
layout: post
title: AP CSA FRQ
description: 2022 - Question 2
type: hacks
courses: {'csa': {'week': 4}}
---

## Textbook Class

You will write a class Textbook, which is a subclass of Book.
A Textbook has an **edition number**, which is a positive integer used to identify **different versions** of the book. 

1. The getBookInfo method, when called on a Textbook, returns a string that also includes the edition information, as shown in the example.
2. Information about the book title and price must be maintained in the Book class. Information about the edition must be maintained in the Textbook class.
3. The Textbook class contains an additional method, canSubstituteFor, which returns true if a Textbook is a valid substitute for another Textbook and returns false otherwise. 
4. The current Textbook is a valid substitute for the Textbook referenced by the parameter of the canSubstituteFor method if the two Textbook objects have the same title and if the edition of the current Textbook is greater than or equal to the edition of the parameter.


```java
public class Book {
    private String title;
    private double price;

    public Book(String bookTitle, double bookPrice) {
        title = bookTitle;
        price = bookPrice;
    }

    // method to get the title of the book
    public String getTitle() {
        return title;
    }

    // method to get the price of the book                                                      
    public double getPrice() {
        return price;
    }

    // method to get book information (title and price)
    public String getBookInfo() {
        return title + " - $" + price;
    }
}
public class Textbook extends Book {  // a subclass Textbook extending the superclass Book
    
    private int edition;  // instance variable to store the edition number of the textbook

    // constructor for Textbook class
    public Textbook(String bookTitle, double bookPrice, int edition) {
        super(bookTitle, bookPrice);  // call the constructor of the superclass (Book), allows to add edition to Book
        this.edition = edition;  // initialize the edition for this textbook
    }

    // getter to retrieve the edition of the textbook
    public int getEdition() {
        return edition;
    }

    // override the method to get book information and include edition
    @Override
    public String getBookInfo() {
        return super.getBookInfo() + " (Edition " + edition + ")";  // append edition information
    }

    // method to check if this textbook can substitute for another textbook
    public boolean canSubstituteFor(Textbook otherTextbook) {
        // check if titles match and this edition is greater than or equal to the other textbook's edition
        return this.getTitle().equals(otherTextbook.getTitle()) && this.edition >= otherTextbook.getEdition();
    }
}
public class Main {
    public static void main(String[] args) {

        // create a textbook instance for calculus
        Textbook calculusTextbook = new Textbook("Calculus", 119.25, 6);
        System.out.println("Title: " + calculusTextbook.getTitle());
        System.out.println("Edition: " + calculusTextbook.getEdition());
        System.out.println("Book Info: " + calculusTextbook.getBookInfo());
        
        // create a textbook instance for physics
        Textbook physicsTextbook = new Textbook("Physics", 89.50, 9);
        System.out.println("\nTitle: " + physicsTextbook.getTitle());
        System.out.println("Edition: " + physicsTextbook.getEdition());
        System.out.println("Book Info: " + physicsTextbook.getBookInfo());

        // check if the physics textbook can substitute for the calculus textbook
        System.out.println("\nCan Calculus textbook substitute for Physics textbook? " + calculusTextbook.canSubstituteFor(physicsTextbook));

        // create a textbook instance for calculus, different edition
        Textbook calculus26Textbook = new Textbook("Calculus", 234.75, 12);

        // check if the calculus textbook can substitute for the other calculus textbook
        System.out.println("\nCan Calculus (26th edition) substitute for Calculus (12th edition) textbook? " + calculus26Textbook.canSubstituteFor(calculusTextbook));
    }
}
Main.main(null)
```

    Title: Calculus
    Edition: 6
    Book Info: Calculus - $119.25 (Edition 6)
    
    Title: Physics
    Edition: 9
    Book Info: Physics - $89.5 (Edition 9)
    
    Can Calculus textbook substitute for Physics textbook? false
    
    Can Calculus (26th edition) substitute for Calculus (12th edition) textbook? true


| Grading  | Points (0 or 1) | Points (0 or 1) |
|----------|-----------------|---|
| Point 1  | I declare class header that is not private and extends from class Book. | 1 |
| Point 2  | I declare the constructor header that defines Textbook | 1 |
| Point 3  | I used super for the first line | 1 |
| Point 4  | I define the variable edition with private | 1 |
| Point 5  | I define at least one of those headers with public | 1 |
| Point 6  | I define getEdition that returns value of edition | 1 |
| Point 7  | The canSubstituteFor method determines correctly | 1 |
| Point 8  | I used super or define getBookInfo | 1 |
| Point 9  | Even though I didn’t use super, I concatenate correctly and access title and price directly | 1 |

Total: 9/9


## ChatGPT Suggestions

- Use final Keyword:
Mark appropriate fields as final

- Proper Exception Handling:
Include try-catch blocks for exception handling

- Properly format Book Price:
Format book price to display with two decimal places

## Improvement

> New Method

Though I was able to get all of the points, I was able to move the printing of book details into a separate method (printBookDetails) to reduce redundancy and enhance code readability in the Main class. I also adjusted the price formatting and used final so that the book prices cannot be changed after they have already been initialized.


```java
public class Book {
    private String title; 
    private double price;

    public Book(String bookTitle, double bookPrice) {
        title = bookTitle;
        price = bookPrice;
    }

    public String getTitle() {
        return title;
    }

    public String getPrice() {
        return String.format("%.2f", price);
    }

    public String getBookInfo() {
        return title + " - $" + getPrice();
    }
}


public class Textbook extends Book {
    private final int edition; // final makes values immutable, cannot be changed after initialization


    public Textbook(String bookTitle, double bookPrice, int edition) {
        super(bookTitle, bookPrice);
        this.edition = edition;
    }


    public int getEdition() {
        return edition;
    }

 
    @Override
    public String getBookInfo() {
        return super.getBookInfo() + " (Edition " + edition + ")";
    }

    public boolean canSubstituteFor(Textbook otherTextbook) {
        return this.getTitle().equals(otherTextbook.getTitle()) && this.edition >= otherTextbook.getEdition();
    }
}

public class Main {
    public static void main(String[] args) {
        Textbook calculusTextbook = new Textbook("Calculus", 119.25, 6);
        printBookDetails(calculusTextbook);

        Textbook physicsTextbook = new Textbook("Physics", 89.50, 9);
        printBookDetails(physicsTextbook);

        System.out.println("\nCan Calculus textbook substitute for Physics textbook? " + calculusTextbook.canSubstituteFor(physicsTextbook));

        Textbook calculus26Textbook = new Textbook("Calculus", 234.75, 12);
        System.out.println("\nCan Calculus (26th edition) substitute for Calculus (12th edition) textbook? " + calculus26Textbook.canSubstituteFor(calculusTextbook));
    }

    private static void printBookDetails(Textbook textbook) {
        System.out.println("Title: " + textbook.getTitle());
        System.out.println("Edition: " + textbook.getEdition());
        System.out.println("Book Info: " + textbook.getBookInfo());
    }
}
Main.main(null)
```

    Title: Calculus
    Edition: 6
    Book Info: Calculus - $119.25 (Edition 6)
    Title: Physics
    Edition: 9
    Book Info: Physics - $89.50 (Edition 9)
    
    Can Calculus textbook substitute for Physics textbook? false
    
    Can Calculus (26th edition) substitute for Calculus (12th edition) textbook? true

