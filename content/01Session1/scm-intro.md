---
title: "Source Code Management Introduction"
linkTitle: "SCM Introduction"
weight: 2
---

### Overview

Let's talk about the most important driver of our devops or DevSecOps program - the management of our source code. One of the core drivers behind code security is evaluating poorly written code. Poorly written code can be many things, so it's always important to ask:

1. Is my code easy to understand?
2. Is my code using the latest dependencies?
3. Is my code efficient?
4. Is my code purposefully written?

Clean code is about writing only the code necessary to accomplish a task as effectively as possible, while also accounting for security concerns such as dependency management and error handling. Let’s explore the concept of clean code in more detail.

#### Clean Code

Clean code principles focus on writing code that is easy to read, understand, and maintain. Key principles include using meaningful names, writing small functions, avoiding duplication, eliminating side effects, and keeping code expressive. Ultimately, the goal is to create code that is both readable for humans and reliable for machines. 

Here's a more detailed breakdown of the key principles:

##### Meaningful Names:
Variables, functions, and classes should have descriptive names that clearly indicate their purpose, making the code self-explanatory. 

##### Small Functions:
Functions should be short and focused, ideally with a single responsibility (Single Responsibility Principle). 

##### Avoid Duplication:
The "DRY (Don't Repeat Yourself)" principle encourages minimizing redundancy and refactoring code to avoid repeating logic. 

##### Eliminate Side Effects:
Functions should ideally have no unintended consequences or effects outside of their intended scope. 

##### Keep Code Expressive:
Code should be clear and concise, using the fewest lines necessary to accomplish the task. 

##### Comments and Documentation:
While code should be largely self-explanatory, comments can be used to explain complex logic or provide additional context. 

##### Consistent Formatting:
Consistent coding style and indentation enhance readability and maintainability. 

##### Testing:
Thorough testing is crucial for ensuring the reliability and correctness of the code. 

##### Error Handling:
Graceful error handling is essential for robust and predictable behavior. 

##### Modularization:
Breaking down code into smaller, independent modules promotes reusability and maintainability. 

##### Dependencies:
Managing dependencies and avoiding excessive dependencies can simplify code. 

##### Readability:
Prioritizing readability over brevity makes code easier to understand and maintain. 

##### Simplicity:
Strive for the simplest solution possible, avoiding unnecessary complexity. 

In this chapter we've talked about taking the first step in securing our code, which is to write meaninfgul, error free code in the first place. Not as easy as it sounds! In the next chapter, we'll discuss repository-specific safeguards for protecting our source code that everyone should be aware of! 