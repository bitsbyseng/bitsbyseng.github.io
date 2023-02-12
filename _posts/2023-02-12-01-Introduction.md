---
layout: single
title:  "01 Introduction to Algorithms"
categories: basic algorithms
tag: [python, algorithm]
---

## Time Complexity (The Big O Notation)
We can predict how long it will take in the worst case scenario. 

Example
* N people visit a restaurant
* There are M menu items and 1 menu
* It takes a person O(M) time to read the menu 
* All the items are served at the same time and each person i takes Ai time to eat
* Each person takes O(P) time to pay
* The time complexity of everyone reading the entire menu = O(NM)
* The time complexity of everyone finishing his meal = O(max(Ai))
* The time complexity of everyone lining up in one line to pay = P(NP)

We can often calculate it by looking at the source or predicting prior to solving the question. 

We must pay attention to the time limit alloted to each problem.

<br>Around 100,000,000 n = 1 second</br>
If N =< 100,000

O(1) -> 1 very fast

O(N) -> 100,000 = 10/10000 seconds

O(N**2) -> 10,000,000,000 => 100 seconds



In reality, up to aroudn 500,000,000N can be executed within a second.

With the Big O Notation, we drop all the constants 
* O(3N**2) = O(N**2)
* O(1/2N**2) = O(N**2)
* O(5) = O(1)

If there are two variables, we drop everything except for the biggest unless the variables are different. 
* O(N**2 + N) = O(N**2)
* O(N**2 + M) = as is

## Stacks
A type of data structure that only allows input and output through one way

Finding Brackets 
(()(())))
* By utilizing the idea of a stack we can pop whenever a pair is complete. 
* If there are value left in the stack, that means that there wasn't a proper number of brackets. 
  
We can do this more easily by using count: 


```python
import sys
trials = int(input())
for i in range(trials):
    cnt = 0
    brackets = sys.stdin.readline().strip()
    for i in brackets:
        if i =='(':
            cnt += 1
        else:
            cnt -= 1
        if cnt < 0: 
            print('NO')
            break
    if cnt == 0:
        print('YES')
    elif cnt > 0: 
        print('NO')
```

Stack Sequence
* Creating a sequence by pushing an popping from a stack

Editor 
* L: Moves the cursor one space to the left. 
* D: Moves the cursor one space to the right. 
* B: Deletes the letter that's left of the cursor. 
* P p: Adds the letter p on the right side of the cursor. 


```python
import sys
letters = sys.stdin.readline().strip()
left = [i for i in letters]
right = []
trials = int(sys.stdin.readline())
for i in range(trials):
    command = sys.stdin.readline().split()
    if command[0] == 'L' and left:
        right.insert(0, left[-1])
        left.pop(-1)
    elif command[0] == 'D' and right:
        left.append(right[0])
        right.pop(0)
    elif command[0] == 'B' and left:
        left.pop(-1)
    elif command[0] == 'P':
        left.append(command[1])
final = left + right
print(''.join(final))
```

This solution goes overtime however. 
