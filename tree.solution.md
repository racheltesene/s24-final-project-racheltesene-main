**Sample solution:**

```csharp
using System;

class TreeNode {
    public int Value;
    public TreeNode Left, Right;

    public TreeNode(int value) {
        Value = value;
        Left = Right = null;
    }
}

class BinarySearchTree {
    public TreeNode Root;

    public BinarySearchTree() {
        Root = null;
    }

    public void Insert(int value) {
        Root = InsertRec(Root, value);
    }

    private TreeNode InsertRec(TreeNode root, int value) {
        if (root == null) {
            root = new TreeNode(value);
            return root;
        }

        if (value < root.Value) {
            root.Left = InsertRec(root.Left, value);
        } else if (value > root.Value) {
            root.Right = InsertRec(root.Right, value);
        }

        return root;
    }

    public void Delete(int value) {
        Root = DeleteRec(Root, value);
    }

    private TreeNode DeleteRec(TreeNode root, int value) {
        if (root == null) {
            return root;
        }

        if (value < root.Value) {
            root.Left = DeleteRec(root.Left, value);
        } else if (value > root.Value) {
            root.Right = DeleteRec(root.Right, value);
        } else {
            if (root.Left == null) {
                return root.Right;
            } else if (root.Right == null) {
                return root.Left;
            }

            root.Value = MinValue(root.Right);
            root.Right = DeleteRec(root.Right, root.Value);
        }

        return root;
    }

    private int MinValue(TreeNode root) {
        int minValue = root.Value;
        while (root.Left != null) {
            minValue = root.Left.Value;
            root = root.Left;
        }
        return minValue;
    }

    public bool Search(int value) {
        return SearchRec(Root, value) != null;
    }

    private TreeNode SearchRec(TreeNode root, int value) {
        if (root == null || root.Value == value) {
            return root;
        }

        if (value < root.Value) {
            return SearchRec(root.Left, value);
        }

        return SearchRec(root.Right, value);
    }

    public void InOrderTraversal() {
        InOrderRec(Root);
        Console.WriteLine();
    }

    private void InOrderRec(TreeNode root) {
        if (root != null) {
            InOrderRec(root.Left);
            Console.Write(root.Value + " ");
            InOrderRec(root.Right);
        }
    }

    public void PreOrderTraversal() {
        PreOrderRec(Root);
        Console.WriteLine();
    }

    private void PreOrderRec(TreeNode root) {
        if (root != null) {
            Console.Write(root.Value + " ");
            PreOrderRec(root.Left);
            PreOrderRec(root.Right);
        }
    }

    public void PostOrderTraversal() {
        PostOrderRec(Root);
        Console.WriteLine();
    }

    private void PostOrderRec(TreeNode root) {
        if (root != null) {
            PostOrderRec(root.Left);
            PostOrderRec(root.Right);
            Console.Write(root.Value + " ");
        }
    }
}

class Program {
    static void Main() {
        BinarySearchTree bst = new BinarySearchTree();
        while (true) {
            Console.WriteLine("1. Insert");
            Console.WriteLine("2. Delete");
            Console.WriteLine("3. Search");
            Console.WriteLine("4. In-order Traversal");
            Console.WriteLine("5. Pre-order Traversal");
            Console.WriteLine("6. Post-order Traversal");
            Console.WriteLine("7. Quit");
            Console.Write("Enter your choice: ");
            int choice = int.Parse(Console.ReadLine());

            if (choice == 7) break;

            switch (choice) {
                case 1:
                    Console.Write("Enter value to insert: ");
                    int insertValue = int.Parse(Console.ReadLine());
                    bst.Insert(insertValue);
                    break;
                case 2:
                    Console.Write("Enter value to delete: ");
                    int deleteValue = int.Parse(Console.ReadLine());
                    bst.Delete(deleteValue);
                    break;
                case 3:
                    Console.Write("Enter value to search: ");
                    int searchValue = int.Parse(Console.ReadLine());
                    bool found = bst.Search(searchValue);
                    Console.WriteLine(found ? "Found" : "Not Found");
                    break;
                case 4:
                    bst.InOrderTraversal();
                    break;
                case 5:
                    bst.PreOrderTraversal();
                    break;
                case 6:
                    bst.PostOrderTraversal();
                    break;
                default:
                    Console.WriteLine("Invalid choice.");
                    break;
            }
        }
    }
}
```