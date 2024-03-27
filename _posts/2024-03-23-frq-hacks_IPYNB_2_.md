---
title: FRQ Hacks
toc: True
comments: True
layout: post
type: hacks
courses: {'csse': {'week': 1}, 'csp': {'week': 1, 'categories': ['4.A']}, 'csa': {'week': 0}, 'labnotebook': {'week': 3}}
---

## FRQ 3

a. Define an arrayList in Java. Explain its significance and usefulness in programming.

An ArrayList is a data structure that resembles a dynamic array and whose size can change dynamically when elements are added or removed. It is more flexible than arrays and is a component of the Java Collections Framework.

b. You need to implement a method `calculateAverageGrade` that takes an arrayList `grades` of integers representing student grades and returns the average of all the elements in the arrayList. Write the method signature and the method implementation. Include comments to explain your code.


```java
import java.util.ArrayList;

public class GradeCalc {
    
    public static double calculateAverageGrade(ArrayList<Integer> grades) {
        int sum = 0;
        
        for (int grade : grades) { // iterate through the ArrayList to calculate the sum
            sum += grade;
        }
        
        double average = (double) sum / grades.size(); // divide sum by number of grades to get average
        
        return average;
    }

    public static void main(String[] args) {
        ArrayList<Integer> studentGrades = new ArrayList<>();
        studentGrades.add(10); // test data
        studentGrades.add(20);
        studentGrades.add(30);
        
        System.out.println("Average grade: " + calculateAverageGrade(studentGrades));
    }
}
GradeCalc.main(null);
```

    Average grade: 20.0


## Question 5

a. Explain the roles and usage of the if statement, while loop, and else statement in Java programming. Provide examples illustrating each.


b. 

You need to implement a method `printGradeStatus` that takes an integer `score` as input and prints "Pass" if the score is greater than or equal to 60, and "Fail" otherwise. Write the method signature and the method implementation. Include comments to explain your code.


```java

```
