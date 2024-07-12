# Introduction to Linked Lists

A linked list is a linear data structure in which elements are stored in nodes. Each node contains data and a reference (or link) to the next node in the sequence. This structure allows for efficient insertion and deletion of elements.

## Node Structure

A node in a linked list typically contains two parts:

Data: Stores the value.
Next: A reference to the next node in the list.
Here's an example of a basic node structure in C#:

```csharp 
public class Node {
    public int Data;
    public Node Next;

    public Node(int data) {
        Data = data;
        Next = null;
    }
}

```

## Types of Linked Lists

### Singly Linked List

A singly linked list is a type of linked list where each node points to the next node in the sequence. The last node points to `null`.

```csharp
public class SinglyLinkedList {
    public Node Head;

    public void Add(int data) {
        Node newNode = new Node(data);
        if (Head == null) {
            Head = newNode;
        } else {
            Node current = Head;
            while (current.Next != null) {
                current = current.Next;
            }
            current.Next = newNode;
        }
    }
}

```

### Doubly Linked List

A doubly linked list has nodes that contain references to both the next and previous nodes, allowing traversal in both directions.

```csharp 
public class DoublyNode {
    public int Data;
    public DoublyNode Next;
    public DoublyNode Previous;

    public DoublyNode(int data) {
        Data = data;
        Next = null;
        Previous = null;
    }
}
```

### Circular Linked List

A circular linked list is a variation where the last node points back to the first node, creating a loop.

```csharp
public class CircularLinkedList {
    public Node Head;

    public void Add(int data) {
        Node newNode = new Node(data);
        if (Head == null) {
            Head = newNode;
            Head.Next = Head;
        } else {
            Node current = Head;
            while (current.Next != Head) {
                current = current.Next;
            }
            current.Next = newNode;
            newNode.Next = Head;
        }
    }
}

```

## Traversal and Manipulation

Traversal involves visiting each node in the list to access or update the data.

### Traversal in Singly Linked List

```csharp
public void Traverse() {
    Node current = Head;
    while (current != null) {
        Console.WriteLine(current.Data);
        current = current.Next;
    }
}
```
### Insertion at the Beginning

```csharp
public void InsertAtBeginning(int data) {
    Node newNode = new Node(data);
    newNode.Next = Head;
    Head = newNode;
}
```

### Deletion of a Node

```csharp
public void DeleteNode(int key) {
    Node temp = Head, prev = null;
    if (temp != null && temp.Data == key) {
        Head = temp.Next;
        return;
    }
    while (temp != null && temp.Data != key) {
        prev = temp;
        temp = temp.Next;
    }
    if (temp == null) return;
    prev.Next = temp.Next;
}
```
## Efficiency of Common Operations

1. Insertion: O(1) at the beginning, O(n) at the end.

2. Deletion: O(1) for the head node, O(n) for other nodes.

3. Searching: O(n).

## Example Problem

### Problem Statement

Reverse a singly linked list.

### Solution

To reverse a linked list, we can iterate through the list and adjust the pointers of each node.

```csharp
public Node Reverse(Node head) {
    Node prev = null, current = head, next = null;
    while (current != null) {
        next = current.Next;
        current.Next = prev;
        prev = current;
        current = next;
    }
    head = prev;
    return head;
}

// Test the function
SinglyLinkedList list = new SinglyLinkedList();
list.Add(1);
list.Add(2);
list.Add(3);
list.Head = Reverse(list.Head);

// Output the reversed list
Node current = list.Head;
while (current != null) {
    Console.WriteLine(current.Data);
    current = current.Next;
}
// Output: 3 2 1
```

## Problem to Solve

### Problem Statement

Write a program to detect a cycle in a linked list.

### Solution

To detect a cycle, we can use Floyd’s Cycle-Finding Algorithm, also known as the tortoise and hare algorithm.

1. Initialize two pointers, slow and fast.

2. Move the slow pointer one step at a time and the fast pointer two steps at a time.

3. If the pointers meet, there is a cycle. If the fast pointer reaches the end, there is no cycle.

```csharp
public bool HasCycle(Node head) {
    if (head == null || head.Next == null) return false;
    Node slow = head, fast = head;
    while (fast != null && fast.Next != null) {
        slow = slow.Next;
        fast = fast.Next.Next;
        if (slow == fast) return true;
    }
    return false;
}

// Test the function
SinglyLinkedList list = new SinglyLinkedList();
list.Add(1);
list.Add(2);
list.Add(3);
// Create a cycle
list.Head.Next.Next.Next = list.Head.Next;

bool hasCycle = HasCycle(list.Head);
Console.WriteLine(hasCycle); // Output: True
```

In this problem, we use the tortoise and hare algorithm to detect a cycle in the linked list efficiently.