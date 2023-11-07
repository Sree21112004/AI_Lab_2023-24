# Ex.No: 11  Planning –  Block World Problem 
### DATE: 07.10.2023                                                                         
### REGISTER NUMBER : 212222060252
### AIM: 
To find the sequence of plan for Block word problem using PDDL  
###  Algorithm:
Step 1 :  Start the program <br>
Step 2 : Create a domain for Block world Problem <br>
Step 3 :  Create a domain by specifying predicates clear, on table, on, arm-empty, holding. <br>
Step 4 : Specify the actions pickup, putdown, stack and un-stack in Block world problem <br>
Step 5 :  In pickup action, Robot arm pick the block on table. Precondition is Block is on table and no other block on specified block and arm-hand empty.<br>
Step 6:  In putdown action, Robot arm place the block on table. Precondition is robot-arm holding the block.<br>
Step 7 : In un-stack action, Robot arm pick the block on some block. Precondition is Block is on another block and no other block on specified block and arm-hand empty.<br>
Step 8 : In stack action, Robot arm place the block on under block. Precondition is Block holded by robot arm and no other block on under block.<br>
Step 9 : Define a problem for block world problem.<br> 
Step 10 : Obtain the plan for given problem.<br> 
     
### Program:
#### domain.pddl
``` 
(define (domain blocksworld) 
(:requirements :strips :equality) 
(:predicates (clear ?x) 
 (on-table ?x) 
 (arm-empty) 
 (holding ?x) 
 (on ?x ?y)) 
(:action pickup 
 :parameters (?ob) 
 :precondition (and (clear ?ob) (on-table ?ob) (arm-empty)) 
 :effect (and (holding ?ob) (not (clear ?ob)) (not (on-table ?ob)) 
 (not (arm-empty)))) 
(:action putdown 
 :parameters (?ob) 
 :precondition (and (holding ?ob)) 
 :effect (and (clear ?ob) (arm-empty) (on-table ?ob) 
 (not (holding ?ob)))) 
(:action stack 
 :parameters (?ob ?underob) 
 :precondition (and (clear ?underob) (holding ?ob)) 
 :effect (and (arm-empty) (clear ?ob) (on ?ob ?underob) 
 (not (clear ?underob)) (not (holding ?ob)))) 
(:action unstack 
 :parameters (?ob ?underob) 
 :precondition (and (on ?ob ?underob) (clear ?ob) (arm-empty)) 
 :effect (and (holding ?ob) (clear ?underob) 
 (not (on ?ob ?underob)) (not (clear ?ob)) (not (arm-empty))))) 
```

### Input 
#### Problem 1: Problem.pddl
```
(define (problem pb1) 
 (:domain blocksworld) 
 (:objects a b) 
 (:init (on-table a) (on-table b) (clear a) (clear b) (arm-empty)) 
 (:goal (and (on a b))))
```
#### Problem 2: Problem2.pddl 
```
(define(problem pb3) 
 (:domain blocksworld) 
 (:objects a b c) 
 (:init (on-table a) (on-table b) (on-table c) 
 (clear a) (clear b) (clear c) (arm-empty)) 
 (:goal (and (on a b) (on b c))))
```
### Output/Plan:
#### Problem 1:

![WhatsApp Image 2023-10-26 at 4 19 57 PM](https://github.com/MaheshS03/AI_Lab_2023-24/assets/128498431/c74579bd-b6ac-4f4d-b1c7-13c1e310f09b)

#### Problem 2:

![WhatsApp Image 2023-10-26 at 4 20 02 PM](https://github.com/MaheshS03/AI_Lab_2023-24/assets/128498431/59731b20-c1c4-4ebb-8ca4-0af301f96b58)

### Result:
Thus the plan was found for the initial and goal state of block world problem.
