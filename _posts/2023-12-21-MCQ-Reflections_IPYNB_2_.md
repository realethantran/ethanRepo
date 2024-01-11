---
toc: True
comments: True
layout: post
title: College Board Quiz Reflection
description: A reflection on this trimester so far (Journey, Learnings, and Discoveries)
type: hacks
courses: {'csa': {'week': 17}}
authors: Ethan Tran
---

# Journey, Learnings, and Discoveries

<span style="font-size: 20px;">During my time working on the sorting algorithm for the car game, I faced challenges and learned about interesting things. My main task was to work on both the backend and frontend for the sorting algorithm race. One important thing I learned this trimester was the use of inheritance in our code. Before, my code did not have a superclass and my code was very redundant, which peer graders and Mr. Mortensen pointed out. From there, I started to work on implementing inheritance code within my team's backend for sorting. This turned out to be very useful, allowing for more organized and efficient code. Inheritance helped my team build on existing code without creating unnecessary mess. Furthermore, my team's lesson on jQuery also allowed me to learn more about it. It was new territory for me, so I had to do more research than expected to prepare for the lesson. The main idea I taught involved Event Methods, which led to some research on sites such as W3Schools and such. As a team, we achieved our goal of creating a racing game that incorporated a really cool simulation of the algorithms for sorting and Fibonacci in the form of a race. Our team made sure to listen to advice given by our each other, peers, as well as from Mr. Mortensen ie. inheritance as previously mentioned and an educational aspect. Outside of class, we setup times to meet and discussed plans and any questions or help via a group chat. In terms of the multiple choice test, I thought that I did not do too bad on it. I missed 4 points meaning that I scored a 35/39, which is about an 89%. I don't think that I did poorly on this quiz and after submitting the test I asked questions and compared results with a good friend and fellow CSA student, Rachit Jaiswal. After the MCQ, we got different questions incorrect and correct so we were able to learn from each other, this was very helpful to understanding what I missed on the exam. Overall, I have really enjoyed this trimester and CSA as a whole so far and cannot wait for what the future holds.</span>

## Corrections 

> Question 7

![image](https://github.com/realethantran/fastpages_EthanT/assets/109186517/2d258438-802f-4709-9c3c-48a9d1408bc9)

- My answer, a, was wrong because it would be the result if the outer loop counter variable, outer, was incremented by 2 for each iteration
- The correct answer, c, is correct because the outer loop iterates six times for when outer is assigned the values 1 through 6. For each iteration, the number of times the inner loop iterates is dependent on the value of outer. When outer is 1, the inner loop iterates from 1 to 6, incrementing by 1 each time, and prints all even numbers followed by a space (2 4 6). When outer is 2, the inner loop iterates from 2 to 6 and prints all even numbers followed by a space (2 4 6). When outer is 3, the inner loop iterates from 3 to 6 and prints all even numbers followed by a space (4 6). When outer is 4, the inner loop iterates from 4 to 6 and prints all even numbers followed by a space (4 6). When outer is 5, the inner loop iterates from 5 to 6 and prints 6 followed by a space. When outer is 6, the inner loop iterates one time and prints 6 followed by a space.

> Question 12

![image](https://github.com/realethantran/fastpages_EthanT/assets/109186517/9a2e28ce-4ec6-44e9-8f7c-7ee2f7de84ef)

- My answer, a, was wrong because the only time x && y is true is when both x and y are true. When x and y are both true, (x || y) is true and !(x ||y) is false. Therefore,  (x && y) && !(x || y) will always be false
- B is the correct answer because using De Morgan’s Law, the value of !(x || y) is equivalent to !x && !y. The only time x && y is true is when both x and y are true. When x and y are both true, !x && !y is false. Therefore, (x && y) && (!x && !y) will always be false as will (x && y) && !(x ||y)

> Question 22

![image](https://github.com/realethantran/fastpages_EthanT/assets/109186517/974f6df0-3f76-48ca-9204-d8cc41b1d519)

- My answer, E, was wrong because numbers[0].length returns the number of columns in numbers and numbers.length returns the number of rows. In this case, the outer loop will loop r from 0 to 3, not including 3. However, r is then used as the row index in printing numbers[r][c] and there are only two rows in numbers. An ArraylndexOutOfBoundsExeception will be thrown when the code attempts to access a third row that does not exist
- A is correct because the outer for loop iterates over every row of numbers and assigns each row to the array row.  The inner loop iterates over the array row accessing each element and assigning it to n. Then n is printed to the screen. In the first iteration of the outer loop, row is equal to {1, 2, 3}, and the inner loop will assign each successive value in row to n and print it to the screen, meaning 123 will be printed. For the second iteration of the outer loop, row is equal to {4, 5, 6}, and the inner loop will assign each successive value in row to n and print it to the screen, meaning 456 will be printed after 123, giving us the output 123456.

> Question 31

![image](https://github.com/realethantran/fastpages_EthanT/assets/109186517/d4e15db5-f391-4845-9f4e-1c07edd0a589)

- My answer, d, was incorrect because it would require the second set of nested loops to initialize row to val – 1, increment both row and col in each iteration inner loop (instead of row being decremented) and changing the condition on the inner loop to col < 5 && row < 5
- Choice E is the correct answer because the first set of nested for loops sets each element in board to “O”. The next for loop starts val at 0 and increments by 1 until val is 4, when val is 5 the loop terminates. When val is even, board is not updated, so nothing happens when val is 0. When val is 1, row is assigned 1 and col is assigned 0. The boolean condition in the while loop is true, so board[1][0] is assigned “X”. Then col is incremented to 1 and row is decremented to 0 and board[0][1] is assigned “X”. Then col is incremented to 2 and row is decremented to -1 and the while loop terminates. When val is 2, nothing changes about board. When val is 3, row is assigned 3 and col is assigned 0. The boolean condition in the while loop is true, so board[3][0] is assigned “X”. Then col is incremented to 1 and row is decremented to 2 and board[2][1] is assigned “X”. Then col is incremented to 2 and row is decremented to 1 and board[1][2] is assigned “X”. Then col is incremented to 3 and row is decremented to 0 and board[0][3] is assigned “X”. Finally, col is incremented to 4 and row is decremented to -1 and the while loop terminates. When val is 4, nothing changes about board.
