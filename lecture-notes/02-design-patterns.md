# 02: Design Patterns

## Overview

**Design Patterns** are general reusable solutions to common problems in software design. They are not finished designs that can be transformed directly into code. They are a description or template for how to solve a problem that can be used in many different situations.

Design patterns can speed the development process by providing tested, proven development paradigms. Effective software design requires considering issues that may not become visible until later in the implementation. Reusing design patterns helps prevent subtle issues that can cause major problems and improves code readability for coders and architects familiar with the patterns.

> **Note**: Design patterns are not a silver bullet to all your problems. Do not try to force them. Bad things are supposed to happen if done so. Remember that design patterns are solutions **to** problems, not solutions **finding** problems, so do not overthink.

---

## KISS Principle

The **KISS** principle states that most systems work best if they are kept simple rather than made complicated. Therefore, simplicity should be a key goal in design, and unnecessary complexity should be avoided.

---

## Types of Design Patterns

Design patterns can be classified into three categories:

1. **Creational Patterns**: These design patterns deal with object creation mechanisms, trying to create objects in a manner suitable to the situation. The basic form of object creation could result in design problems or added complexity to the design. **Creational design patterns** solve this problem by controlling the object-creation process.

2. **Structural Patterns**: These design patterns deal with object composition. They describe how classes and objects can be composed to form larger structures. **Structural design patterns** simplify the structure by identifying the relationships.

3. **Behavioral Patterns**: These design patterns deal with object collaboration. They describe how objects interact to form larger systems. **Behavioural design patterns** identify common communication patterns between objects and realise these patterns.

---

## Patterns in Unity

1. **Game loop**: The game loop is a programming pattern that controls the flow of the game. It is a loop that runs continuously and updates the game state. The game loop is responsible for updating the game state, rendering the game, and handling user input.

2. **Prototype**: The prototype pattern is a creational pattern that is used to create a new object by copying an existing object. The prototype pattern is useful when creating new objects is expensive or when the object creation process is complex. 

What is an example of this pattern in **Unity**? 

<details>

<summary>
Click here to see the answer
</summary>

Unity's prefab system is an example of the prototype pattern. Prefabs are used to create new objects by copying an existing object. Prefabs are useful when creating new objects is expensive or when the object creation process is complex.

</details>

3. **Component**: The component pattern is a structural pattern that is used to create complex objects by combining simpler objects. The component pattern is useful when you want to create objects that are composed of other objects.

What is an example of this pattern in **Unity**?

<details>

<summary>Click here to see the answer
</summary>
Unity provides a component-based architecture that allows you to create complex objects by combining simpler objects. For example, you can create a player object by combining a mesh renderer, a collider, and a script component.
</details>

---

## Design Patterns

Let us digest this document - [Design Patterns in Unity](https://bit.ly/4kc3EnQ).

---

## Exercises

Learning to use AI tools is an important skill. While AI tools are powerful, you **must** be aware of the following:

- If you provide an AI tool with a prompt that is not refined enough, it may generate a not-so-useful response
- Do not trust the AI tool's responses blindly. You **must** still use your judgement and may need to do additional research to determine if the response is correct
- Acknowledge what AI tool you have used. In the assessment's repository **README.md** file, please include what prompt(s) you provided to the AI tool and how you used the response(s) to help you with your work
---

### Task One

In this task, you will use a project from a course you have previously taken. Identify at least one example where you have used a design pattern. Describe the design pattern you used and how it helped you solve a problem.

Share the design pattern you used and how it helped you solve a problem [here](https://github.com/otago-polytechnic-bit-courses/ID737001-game-development/discussions/3)

---

### Task Two

Explain how the following design patterns can be implemented in **Pong**:

1. **State**
2. **Strategy**

Share your explanation [here](https://github.com/otago-polytechnic-bit-courses/ID737001-game-development/discussions/3)

---

### Task Three

You will be provided with a **Unity** project that contains **Pong**. Review each file and identify any issues relating to the **SOLID** principles and code smells. Refactor the code to address these issues.

---

### Task Four

In **Pong**, use the following resource - https://youtu.be/aUi9aijvpgs?si=nZ8eXWad94hnbK69 to implement a high score save and load system using the **Singleton** pattern.

---

### Submission

Create a new pull request and assign **grayson-orr** to review your practical submission. Please do not merge your own pull request.

---
