---
toc: True
comments: True
layout: post
title: Scope and Access of a Class
description: Lesson for scope and access of a class
type: tangibles
courses: {'csa': {'week': 28}}
---

# 5.8 Scope and Access

## Scope

- Local variables: variables declared in body of constructors and methods, only use within constructor or method, can’t be declared public or private
- If local variable named same as instance variable, within that method the local variable will be referred to instead of the instance variable
- Formal parameters and variables declared in a method or constructor can only be used within that method or constructor

## Access 

- Private: Variables or methods marked as private are accessible only within the class in which they are declared. This provides the highest level of encapsulation and restricts access from outside the class.
- Package/Default: If no access modifier is specified, the default access level is package-private, also known as default access. This allows access within the same package but restricts access from classes outside the package.
- Public: Public members are accessible from any other class. They provide the least restrictive access and are commonly used for methods and variables that need to be accessed from other classes.

### Example


```python
public class Bowler{
    private int totalPins;
    private int games;
   
    public Bowler(int pins){
        totalPins = pins; // this keyword
        games = 3;
    }

    public void update (int game1, int game2, int game3) {
        // local variable here is newPins
        int newPins = game1 + game2 + game3;
        totalPins += newPins;
        games += 3;
    }
}
```

# Questions


```python
public class Car {
    public String color;
    private int speed;

    public Car(String color, int speed) {
    }

    public void drive(boolean fourWheel) {
    }
}

public class BuyCar {
    public static void main(String[]args) {
        Car carObject = new Car("blue", 70);
        String carColor = carObject.color;
    }
}

```

For the above code segment, please write in the comments if each variable is accessible in each specified method. If the variable can be accessed in a method/class, write that. If it can't be accessed, explain why. 

## FRQ

In this FRQ, you are to create the Counter Java class that encapsulates the behavior of a counter. This counter can increase, decrease, and provide its current count. 


```python
public class SimpleCounter {

    private int count; // to store current count

    public SimpleCounter() {
        // Initialize count to 0
        this.count = 0;
    }

    public void increment() {
        // implementation to increment the count by 1
    }

    public void decrement() {
        // implementation to decrement the count but ensure it doesn't go below 0
    }

    public int getCount() {
        // Returns the current count
        return 0; // Placeholder return value, adjust accordingly
    }
}
```

Feel free to add any additional methods that you deem necessary (potential extra points). You can also get extra points by explaining the scope and access of variables, whether they are the ones provided or ones that you make on your own. 
