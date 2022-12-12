---
layout: page
title: Exercises Ch. 4
description: Select exercises from Python Crash Course
---

## Python Crash Course Chapter 4


```python
pizzas = ["Buffalo Chicken Pizza", "Cheese Pizza", "Any Pizza"]
for p in pizzas:
    print("I really like " + p.lower() + ".")
print("But, " + pizzas[0].lower() + " is my favorite kind of pizza!")
```

    I really like buffalo chicken pizza.
    I really like cheese pizza.
    I really like any pizza.
    But, buffalo chicken pizza is my favorite kind of pizza!
    


```python
animals = ["Dog", "Cat", "Bear"]
for a in animals:
    print(a.title() + "s are mammals.")
print("All of these animals are mammals!")
```

    Dogs are mammals.
    Cats are mammals.
    Bears are mammals.
    All of these animals are mammals!
    


```python
for i in range(1,21):
    print(i)
```

    1
    2
    3
    4
    5
    6
    7
    8
    9
    10
    11
    12
    13
    14
    15
    16
    17
    18
    19
    20
    


```python
odds = []
for i in range(1,21,2):
    odds.append(i)
print(odds)
```

    [1, 3, 5, 7, 9, 11, 13, 15, 17, 19]
    


```python
print(f"The first three items in the list are: {odds[:3]}")
print(f"The middle four items in the list are: {odds[3:7]}")
print(f"The last three items in the list are: {odds[-3:]}")
```

    The first three items in the list are: [1, 3, 5]
    The middle four items in the list are: [7, 9, 11, 13]
    The last three items in the list are: [15, 17, 19]
    


```python
friends_pizzas = pizzas.copy()
pizzas.append("Chicken Pizza")
friends_pizzas.append("Pepperoni Pizza")

print("My favorite pizzas are:")
for p in pizzas:
    print(p.title())
print()
    
print("My friend's favorite pizzas are:")
for p in friends_pizzas:
    print(p.title())

```

    My favorite pizzas are:
    Buffalo Chicken Pizza
    Cheese Pizza
    Any Pizza
    Chicken Pizza
    
    My friend's favorite pizzas are:
    Buffalo Chicken Pizza
    Cheese Pizza
    Any Pizza
    Pepperoni Pizza
    
