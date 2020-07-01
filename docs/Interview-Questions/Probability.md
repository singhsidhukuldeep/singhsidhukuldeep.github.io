---
title: Probability Questions
description: Home page for the platform for Data Science Interview Questions 
---

# Probability Interview Questions

![Total Questions](https://img.shields.io/badge/Total%20Questions-1-blue?style=flat&labelColor=black&color=blue)
![Unanswered Questions](https://img.shields.io/badge/Unanswered%20Questions-0-blue?style=flat&labelColor=black&color=yellow)
![Answered Questions](https://img.shields.io/badge/Answered%20Questions-1-blue?style=flat&labelColor=black&color=success)


---

## Average score on a dice role of at most 3 times

**Question**

Consider a fair 6-sided dice. 
Your aim is to get the highest score you can, in at-most 3 roles.

A score is defined as the number that appears on the face of the dice facing up after the role. 
You can role at most 3 times but every time you role it is up to you to decide whether you want to role again.

The last score will be counted as your final score.

- Find the average score if you rolled the dice only once?
- Find the average score that you can get with at most 3 roles?
- If the dice is fair, why is the average score for at most 3 roles and 1 role not the same?

**Answer**

If you role a fair dice once you can get:

| Score  | Probability  |
|:-:|:-:|
| 1 | 1/6 |
| 2 | 1/6 |
| 3 | 1/6 |
| 4 | 1/6 |
| 5 | 1/6 |
| 6 | 1/6 |


So your average score with one role is: 

`sum of(score * scores's probability)` = (1+2+3+4+5+6)*(1/6) = (21/6) = 3.5

__The average score if you rolled the dice only once is 3.5__

For at most 3 roles, let's try back-tracking. Let's say just did your second role and you have to decide whether to do your 3rd role!

We just found out if we role dice once on average we can expect score of 3.5. So we will only role the 3rd time if score on 2nd role is less than 3.5 i.e (1,2 or 3)

Possibilities

| 2nd role score  | Probability  | 3rd role score  | Probability  |
|:-:|:-:|:-:|:-:|
| 1 | 1/6 | 3.5 | 1/6 |
| 2 | 1/6 | 3.5 | 1/6 |
| 3 | 1/6 | 3.5 | 1/6 |
| 4 | 1/6 | NA | We won't role|
| 5 | 1/6 | NA | 3rd time if we|
| 6 | 1/6 | NA | get score >3 on 2nd|

So if we had 2 roles, average score would be:

```
[We role again of current score is less than 3.4]
(3.5)*(1/6) + (3.5)*(1/6) + (3.5)*(1/6) 
+
(4)*(1/6) + (5)*(1/6) + (6)*(1/6) [Decide not to role again]
=
1.75 + 2.5 = 4.25
```

The average score if you rolled the dice twice is 4.25

So now if we look from the perspective of first role. We will only role again if our score is less than 4.25 i.e 1,2,3 or 4

Possibilities

| 1st role score  | Probability  | 2nd and 3rd role score  | Probability  |
|:-:|:-:|:-:|:-:|
| 1 | 1/6 | 4.25 | 1/6 |
| 2 | 1/6 | 4.25 | 1/6 |
| 3 | 1/6 | 4.25 | 1/6 |
| 4 | 1/6 | 4.25 | 1/6 |
| 5 | 1/6 | NA | We won't role again if we|
| 6 | 1/6 | NA | get score >4.25 on 1st|

So if we had 3 roles, average score would be:

```
[We role again of current score is less than 4.25]
(4.25)*(1/6) + (4.25)*(1/6) + (4.25)*(1/6) + (4.25)*(1/6) 
+
(5)*(1/6) + (6)*(1/6) [[Decide not to role again]
=
17/6 + 11/6 = 4.66
```
__The average score if you rolled the dice only once is 4.66__

The average score for at most 3 roles and 1 role is not the same because although the dice is fair the event of rolling the dice is no longer __independent__.
The scores would have been the same if we rolled the dice 2nd and 3rd time without considering what we got in the last roll i.e. if the event of rolling the dice was independent.


---
