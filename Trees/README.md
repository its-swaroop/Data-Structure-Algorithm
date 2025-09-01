# 🌳 Trees – Complete Chapter Notes

---

## 1. Introduction to Trees

* **Tree**: a hierarchical data structure made of nodes.
* **Terminology**:

  * **Root** → topmost node.
  * **Parent** → node with children.
  * **Child** → node connected downward.
  * **Leaf** → node with no children.
  * **Edge** → link between nodes.
  * **Depth** → distance from root.
* Types of Trees:

  * **Full tree**: every node has 0 or 2 children.
  * **Perfect tree**: completely filled, all leaves at the same level.
  * **Complete tree**: filled level by level, with last level filled from left to right.

---

## 2. Binary Search Trees (BST)

* A **Binary Tree** has at most 2 children per node.
* A **Binary Search Tree (BST)** follows ordering rules:

  * Left child < Parent < Right child.
  * All nodes in the left subtree are smaller.
  * All nodes in the right subtree are larger.

Example:

```
      47
     /  \
   21    76
  / \   /  \
18  27 52  82
```

---

## 3. BST Big-O Analysis

### Average Case (Balanced Tree)

* **Search (contains)** → O(log n)
* **Insert** → O(log n)
* **Remove** → O(log n)

### Worst Case (Unbalanced Tree, like linked list)

* O(n) for all operations.

**Comparison:**

* Linked List search = O(n)
* ArrayList search = O(log n) only if sorted + binary search.
* BST shines because it combines efficient insert + search when balanced.

---

## 4. BST Constructor (Setup)

In Java-style pseudocode:

```java
class Node {
    int value;
    Node left;
    Node right;

    Node(int value) {
        this.value = value;
    }
}

class BST {
    Node root;

    BST() {
        root = null;  // start with empty tree
    }
}
```

* Each **Node** stores a value + pointers to `left` and `right`.
* **BST root** initially `null` (empty).

---

## 5. Insert – Conceptual Steps

To insert into a BST:

1. Create a new node.
2. If tree is empty → new node = root.
3. Otherwise, start at root and compare:

   * If value < current → go left.
   * If value > current → go right.
   * Repeat until empty spot found.
4. Place the new node in that spot.

⚠️ Duplicate handling:

* Some implementations reject duplicates.
* Others allow but define rules (e.g., put duplicates on right).

---

## 6. Insert – Code Implementation

```java
public boolean insert(int value) {
    Node newNode = new Node(value);
    if (root == null) {
        root = newNode;
        return true;
    }
    Node temp = root;
    while (true) {
        if (newNode.value == temp.value) return false; // no duplicates
        if (newNode.value < temp.value) {
            if (temp.left == null) {
                temp.left = newNode;
                return true;
            }
            temp = temp.left;
        } else {
            if (temp.right == null) {
                temp.right = newNode;
                return true;
            }
            temp = temp.right;
        }
    }
}
```

* Iterative approach (no recursion).
* Returns `true` if inserted, `false` if duplicate.

---

## 7. Contains – Conceptual Steps

* To check if a value exists in the BST:

  1. Start at the root.
  2. While current node isn’t null:

     * If value == current → return true.
     * If value < current → go left.
     * If value > current → go right.
  3. If you reach `null`, value not found → return false.

---

## 8. Contains – Code Implementation

```java
public boolean contains(int value) {
    Node temp = root;
    while (temp != null) {
        if (value < temp.value) {
            temp = temp.left;
        } else if (value > temp.value) {
            temp = temp.right;
        } else {
            return true;  // found it
        }
    }
    return false;  // not found
}
```

* Iterative, efficient lookup.
* Runs in O(log n) for balanced trees, O(n) worst-case.

---

# 🔑 Chapter Summary

* **Trees** = hierarchical data structure, important for efficient search/insert.
* **BST Rules**: left < parent < right.
* **Big-O**: log n average, n worst case if unbalanced.
* **Constructor**: starts with `root = null`.
* **Insert**: iterative placement, rejects duplicates.
* **Contains**: standard search, returns boolean.

---

See you next time!
