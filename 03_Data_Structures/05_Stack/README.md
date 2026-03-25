# 1. Introduction to Stack

A **Stack** is a **linear data structure** that follows the **LIFO principle (Last In First Out)**.

This means the **last element inserted into the stack is the first element to be removed**.

### Example

Think of a **stack of plates**:

* You place a plate on the top.
* You remove the plate from the top.

So the last plate placed is the first plate removed.

---

# 2. Basic Stack Operations

A stack supports several basic operations.

## 1. Push

Push operation is used to **insert an element into the stack**.

**Algorithm**

```
if TOP == MAX-1
    Stack Overflow
else
    TOP = TOP + 1
    STACK[TOP] = ITEM
```

**Example**

Push 10, 20, 30

Stack becomes:

```
TOP → 30
       20
       10
```

---

## 2. Pop

Pop operation removes the **top element from the stack**.

**Algorithm**

```
if TOP == -1
    Stack Underflow
else
    ITEM = STACK[TOP]
    TOP = TOP - 1
```

Example:

Before Pop:

```
TOP → 30
       20
       10
```

After Pop:

```
TOP → 20
       10
```

---

## 3. Peek (Top)

Peek operation **returns the top element without removing it**.

```
if TOP == -1
    Stack Empty
else
    print STACK[TOP]
```

---

## 4. isEmpty()

Checks whether stack is empty.

```
if TOP == -1
    return TRUE
else
    return FALSE
```

---

## 5. isFull()

Checks whether stack is full.

```
if TOP == MAX-1
    return TRUE
else
    return FALSE
```

---

# 3. Applications of Stack

1. 📌 **Expression Evaluation (Infix, Prefix, Postfix)**
- Stacks play a crucial role in evaluating mathematical expressions. For example, when you write an expression like A + B × C, the computer uses a stack to convert it into postfix form (ABC×+) and then evaluates it. This ensures the correct order of operations (B × C first, then addition). Without stacks, handling such expressions would be complex and inefficient.

2. 📌 **Function Calls (Call Stack)**
- Whenever a function is called in a program, it is pushed onto the stack. If that function calls another function, the new function is added on top. Once execution is complete, functions are popped from the stack in reverse order. This mechanism is known as the call stack, and it ensures smooth program execution, especially in recursive functions like factorial or Fibonacci.

3. 📌 **Undo/Redo Operations**
- Stacks are widely used in applications that support undo and redo operations. For example, when you press Ctrl + Z, the last action is popped from the undo stack. If you press Ctrl + Y, the action is retrieved from the redo stack. This dual-stack system allows users to navigate back and forth through their actions efficiently.

4. 📌 **Parenthesis Checking (Syntax Checking)**
- Stacks are essential for checking whether parentheses in an expression are balanced. When an opening bracket is encountered, it is pushed onto the stack. When a closing bracket appears, the stack is checked and popped. If everything matches correctly, the expression is valid. This technique is heavily used in compilers and IDEs to detect syntax errors in code.

5. 📌 **Backtracking (Maze, Browser History)**
- Backtracking is a problem-solving technique where stacks are extremely useful. For instance, while solving a maze, each path is pushed onto the stack. If a dead end is reached, the algorithm pops the last path and tries a new one. Similarly, web browsers use stacks to store history, allowing users to go back to previously visited pages.

---

# 4. Types of Expressions

There are **three types of expressions**.

| Type    | Example |
| ------- | ------- |
| Infix   | A + B   |
| Prefix  | + A B   |
| Postfix | A B +   |

---

# 5. Prefix Expression

In **Prefix notation**, the **operator appears before operands**.

### Example

```
+ A B
```

Means

```
A + B
```

Another example:

```
* + A B C
```

Means

```
(A + B) * C
```

---

# 6. Postfix Expression

In **Postfix notation**, the **operator appears after operands**.

### Example

```
A B +
```

Means

```
A + B
```

Another example:

```
A B + C *
```

Means

```
(A + B) * C
```

---

# 7. Evaluation of Postfix Expression Using Stack

### Algorithm

1. Scan expression from **left to right**
2. If operand → **push into stack**
3. If operator:

   * Pop two operands
   * Perform operation
   * Push result back
4. Final result will be at **top of stack**

---

### Example

Evaluate:

```
5 6 2 + *
```

Step-by-step:

| Step   | Stack |
| ------ | ----- |
| Push 5 | 5     |
| Push 6 | 5 6   |
| Push 2 | 5 6 2 |
| +      | 5 8   |
| *      | 40    |

Result = **40**

---

# 8. Evaluation of Prefix Expression Using Stack

### Algorithm

1. Scan expression **from right to left**
2. If operand → **push into stack**
3. If operator:

   * Pop two operands
   * Perform operation
   * Push result back
4. Final result is **top of stack**

---

### Example

Evaluate:

```
* + 5 6 2
```

Step-by-step:

Scan Right → Left

| Step   | Stack |
| ------ | ----- |
| Push 2 | 2     |
| Push 6 | 2 6   |
| Push 5 | 2 6 5 |
| +      | 2 11  |
| *      | 22    |

Result = **22**

---

# 9. Advantages of Prefix and Postfix

1. No need of parentheses
2. Easy to evaluate using stack
3. Faster computation for machines
4. Removes ambiguity

---

# 10. Stack Implementation (Python)

```
MAX = 5
stack = [0] * MAX
top = -1

def push(x):
    global top
    if top == MAX - 1:
        print("Stack Overflow")
    else:
        top += 1
        stack[top] = x

def pop():
    global top
    if top == -1:
        print("Stack Underflow")
    else:
        print("Deleted:", stack[top])
        top -= 1

def display():
    global top
    if top == -1:
        print("Stack is empty")
    else:
        for i in range(top, -1, -1):
            print(stack[i], end=" ")
        print()

# Main function
push(10)
push(20)
push(30)
display()
```

---

# 11. Summary:
Always remember these points:

* Stack follows **LIFO**
* Two main operations: **Push and Pop**
* **Overflow** occurs when stack is full
* **Underflow** occurs when stack is empty
* **Postfix evaluation → Left to Right**
* **Prefix evaluation → Right to Left**

---
