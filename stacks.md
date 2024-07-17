# Introduction to Stacks

A stack is a linear data structure that follows a particular order for operations. Think of a stack like a stack of plates: you can only take the top plate off the stack or add a new plate to the top. This data structure is used in various programming scenarios for its simplicity and efficiency.

## LIFO Principle

The LIFO (Last In, First Out) principle is the main characteristic of a stack. It means that the last element added to the stack will be the first one to be removed. Imagine a stack of books: the last book you put on the stack is the first one you take off.

## Common Operations (Push, Pop, Peek)

1. Push: Adds an element to the top of the stack.

```csharp 
stack.Push(10);
```
2. Pop: Removes and returns the top element of the stack.

```csharp
int topElement = stack.Pop();
```
3. Peek: Returns the top element of the stack without removing it.

```csharp
int topElement = stack.Peek();
```

## Use Cases

Stacks are used in various scenarios, including:

1. Function Call Management: When a function calls another function, the current function’s state is saved on the stack.

2. Undo Mechanisms: Applications like text editors use stacks to keep track of changes, allowing users to undo actions.

3. Expression Evaluation: Stacks are used to evaluate expressions and convert expressions from one notation to another (e.g., infix to postfix).

## Efficiency of Common Operations

The common operations of a stack (push, pop, and peek) are very efficient. All these operations have a time complexity of O(1), meaning they take constant time regardless of the number of elements in the stack.

## Example Problem
Let’s consider a simple problem: checking for balanced parentheses in an expression.

## Problem Statement
Given an expression containing various types of parentheses ((), {}, []), determine if the parentheses are balanced.

## Solution

We can use a stack to solve this problem efficiently.

1. Traverse the expression from left to right.

2. If the current character is an opening parenthesis (`(`, `{`, `[`), push it onto the stack.

3. If the current character is a closing parenthesis (`)`, `}`, `]`), check if the stack is empty or if the top of the stack is not the matching opening parenthesis. If either condition is true, the parentheses are not balanced.

4. After processing all characters, if the stack is not empty, the parentheses are not balanced.

Here is the code in C#:

```csharp
bool AreParenthesesBalanced(string expression) {
    Stack<char> stack = new Stack<char>();
    foreach (char c in expression) {
        if (c == '(' || c == '{' || c == '[') {
            stack.Push(c);
        } else if (c == ')' || c == '}' || c == ']') {
            if (stack.Count == 0) return false;
            char top = stack.Pop();
            if ((c == ')' && top != '(') ||
                (c == '}' && top != '{') ||
                (c == ']' && top != '[')) {
                return false;
            }
        }
    }
    return stack.Count == 0;
}


```
## Problem to Solve

### Problem Statement
Write a program to reverse a string using a stack.

### Solution

You can check your code with the solution here: [Solution](stacks.solution.md)


