---
title: Workshop 2 Hacks
description: Classes Workshop Hacks
toc: True
layout: post
type: hacks
comments: True
---

# Free Response Questions

## Question 2 - Writing Classes:

(a) Describe the different features needed to create a class and what their purpose is.

- Name of Class: The identifier used to define a class and indicate the kinds of objects that can be instantiated from it is its name

- Instance Variables: Used to store data in an object

- Encapsulation: Preserves data integrity and avoid undesired outside interference, groups data (instance variables) and methods into a single unit

- Methods: Define the behavior of objects by encapsulating operations that can be performed on the object's data, facilitating interaction and functionality

- Constructor:Initialize object state by assigning initial values to instance variables or performing setup tasks, automatically called upon object creation and sharing the same name as the class

- Abstraction: Simplifies complex systems by focusing on essential features while hiding unnecessary implementation details, achieved through abstract classes and interfaces in Java

- Polymorphism: Allows objects to take on different forms or behave differently based on their types, facilitated by method overriding and overloading in Java

- Inheritance: Establishes hierarchical relationships between classes, allowing subclasses to inherit properties and behaviors from a superclass, promoting code reuse and extending functionality

(b) Code:

Create a Java class BankAccount to represent a simple bank account. This class should have the following attributes:
- accountHolder (String): The name of the account holder.
balance (double): The current balance in the account.
Implement the following mutator (setter) methods for the BankAccount class:
- setAccountHolder(String name): Sets the name of the account holder.
- deposit(double amount): Deposits a given amount into the account.
- withdraw(double amount): Withdraws a given amount from the account, but only if the withdrawal amount is less than or equal to the current balance.
Ensure that the balance is never negative.


```Java
public class BankAccount {
    private String accountHolder;
    private double balance;

    public BankAccount(String accountHolder, double balance) { 
        this.accountHolder = accountHolder; 
        this.balance = balance; 
    }

    public String getAccountHolder() {
        return accountHolder;
    }

    public void setAccountHolder(String accountHolder) { 
        this.accountHolder = accountHolder; // update accountHolder
    }

    public void deposit(double amount) { 
        if (amount > 0) { // check if amount is positive
            balance += amount; // add amount to balance
            System.out.println(amount + " deposited"); // print deposit message
        } else {
            System.out.println("Invalid amount deposited"); //error message
        }
    }

    public void withdraw(double amount) {
        if (amount > 0 && amount <= balance) { // check if withdrawal amount is positive and less than or equal to balance
            balance -= amount; // subtract amount from balance
            System.out.println(amount + " withdrawn successfully."); 
        } else {
            System.out.println("Insufficient balance or invalid withdrawal amount.");
        }
    }


    // main method for testing
    public static void main(String[] args) {
        BankAccount account = new BankAccount("SGA", 5000.0);
        System.out.println("Account of " + account.getAccountHolder() + " Current balance: " + account.balance );
        account.deposit(1500.0);
        System.out.println("Balance after deposit: " + account.balance);
        account.withdraw(2500.0);
        System.out.println("Balance after withdrawal: " + account.balance);
    }
}
BankAccount.main(null);
```

    Account of SGA Current balance: 5000.0
    1500.0 deposited
    Balance after deposit: 6500.0
    2500.0 withdrawn successfully.
    Balance after withdrawal: 4000.0


## Question 3 - Instantiation of a Class

(a) Explain how a constructor works, including when it runs and what generally is done within a constructor.

When an object of that class is created using the new keyword, Java automatically invokes a special method called a constructor within that class. It is mainly used to initialize the object's state via setting initial values to it's variables, executing at the point of object creation. Constructors frequently establish default values or initialize variables based on parameters passed to them during object creation. They can also be overloaded, providing for numerous ways to create an object.

(b) Create an example of an overloaded constructor within a class. You must use at least three variables. Include the correct initialization of variables and correct headers for the constructor. Then, run the constructor at least twice with different variables and demonstrate that these two objects called different constructors. 


```Java
public class Car {
    private String brand;
    private String model;
    private int year;
    private String engine;

    public Car() {
        // setting default values
        this.brand = "Unknown";
        this.model = "Unknown";
        this.year = 0;
        this.engine = "Unknown";
    }

    public Car(String brand, String model, int year, String engine) {
        // initializing with provided values
        this.brand = brand;
        this.model = model;
        this.year = year;
        this.engine = engine;
    }

    // method to display car details
    public void displayDetails() {
        System.out.println("Manufacturer: " + brand);
        System.out.println("Model: " + model);
        System.out.println("Year: " + year);
        System.out.println("Engine: " + engine);
        System.out.println();
    }

    public static void main(String[] args) {
        // car test data
        Car car1 = new Car("Lexus", "ISF", 2011, "V8");
        Car car2 = new Car("Kia", "Rio", 2019, "Inline-4");

        // display car 1 and car 2 details
        System.out.println("Car 1:");
        car1.displayDetails();

        System.out.println("Car 2:");
        car2.displayDetails();
    }
}
Car.main(null);
```

    Car 1:
    Manufacturer: Lexus
    Model: ISF
    Year: 2011
    Engine: V8
    
    Car 2:
    Manufacturer: Kia
    Model: Rio
    Year: 2019
    Engine: Inline-4
    


## Question 5 - Inheritence:

Situation: You are developing a program to manage a zoo, where various types of animals are kept in different enclosures. To streamline your code, you decide to use inheritance to model the relationships between different types of animals and their behaviors.

(a) Explain the concept of inheritance in Java. Provide an example scenario where inheritance is useful.

(b) Code:

You need to implement a Java class hierarchy to represent different types of animals in the zoo. Create a superclass Animal with basic attributes and methods common to all animals, and at least three subclasses representing specific types of animals with additional attributes and methods. Include comments to explain your code, specifically how inheritance is used.



```Java

```
