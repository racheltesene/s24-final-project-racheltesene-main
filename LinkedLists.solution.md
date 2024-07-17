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