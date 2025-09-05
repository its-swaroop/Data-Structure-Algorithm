# 📘 Linked Lists in Java – Complete Chapter Notes


## 1. Introduction to Linked Lists

* **Linked List**: linear data structure made of **nodes**.
* **Node**: contains a value + pointer to next node.
* **Head**: first node.
* **Tail**: last node (points to null).
* Nodes are **not stored contiguously in memory**.
* Unlike arrays, **no direct indexing**.

### Node Structure

```java
class Node {
    int value;
    Node next;

    Node(int value) {
        this.value = value;
        this.next = null;
    }
}
```

### LinkedList Class Fields

```java
class LinkedList {
    private Node head;
    private Node tail;
    private int length;
}
```

---

## 2. Append (Add to End)

```java
public void append(int value) {
    Node newNode = new Node(value);
    if (length == 0) {
        head = newNode;
        tail = newNode;
    } else {
        tail.next = newNode;
        tail = newNode;
    }
    length++;
}
```

* Adds new node at end.
* **O(1)** time.

---

## 3. Prepend (Add to Front)

```java
public void prepend(int value) {
    Node newNode = new Node(value);
    if (length == 0) {
        head = newNode;
        tail = newNode;
    } else {
        newNode.next = head;
        head = newNode;
    }
    length++;
}
```

* Adds new node at start.
* **O(1)** time.

---

## 4. Remove Last

```java
public Node removeLast() {
    if (length == 0) return null;
    Node temp = head;
    Node pre = head;
    while (temp.next != null) {
        pre = temp;
        temp = temp.next;
    }
    tail = pre;
    tail.next = null;
    length--;
    if (length == 0) {
        head = null;
        tail = null;
    }
    return temp;
}
```

* Traverse to second-last node.
* **O(n)** time (must walk list).

---

## 5. Remove First

```java
public Node removeFirst() {
    if (length == 0) return null;
    Node temp = head;
    head = head.next;
    temp.next = null;
    length--;
    if (length == 0) tail = null;
    return temp;
}
```

* Removes first node.
* **O(1)** time.

---

## 6. Get (By Index)

```java
public Node get(int index) {
    if (index < 0 || index >= length) return null;
    Node temp = head;
    for (int i = 0; i < index; i++) {
        temp = temp.next;
    }
    return temp;
}
```

* Traverses until index found.
* **O(n)** time.

---

## 7. Set (Update Value)

```java
public boolean set(int index, int value) {
    Node temp = get(index);
    if (temp != null) {
        temp.value = value;
        return true;
    }
    return false;
}
```

* Reuses `get()` method.
* **O(n)** time.

---

## 8. Insert (At Index)

```java
public boolean insert(int index, int value) {
    if (index < 0 || index > length) return false;
    if (index == 0) {
        prepend(value);
        return true;
    }
    if (index == length) {
        append(value);
        return true;
    }
    Node newNode = new Node(value);
    Node temp = get(index - 1);
    newNode.next = temp.next;
    temp.next = newNode;
    length++;
    return true;
}
```

* Handles start, end, and middle cases.
* **O(1)** for start/end, **O(n)** for middle.

---

## 9. Remove (By Index)

```java
public Node remove(int index) {
    if (index < 0 || index >= length) return null;
    if (index == 0) return removeFirst();
    if (index == length - 1) return removeLast();
    Node prev = get(index - 1);
    Node temp = prev.next;
    prev.next = temp.next;
    temp.next = null;
    length--;
    return temp;
}
```

* Returns removed node.
* **O(n)** time.

---

## 10. Reverse (In-Place)

```java
public void reverse() {
    Node temp = head;
    head = tail;
    tail = temp;
    Node before = null;
    Node after;
    for (int i = 0; i < length; i++) {
        after = temp.next;
        temp.next = before;
        before = temp;
        temp = after;
    }
}
```

* Swaps head and tail, reverses links.
* Uses `before`, `after`, `temp` pointers.
* **O(n)** time.

---

# 🔑 Chapter Summary

* Linked Lists store elements dynamically via nodes.
* **Append/Prepend**: O(1).
* **Remove Last**: O(n), must traverse.
* **Remove First**: O(1).
* **Get/Set**: O(n).
* **Insert/Remove by index**: O(n) for middle, O(1) for ends.
* **Reverse**: in-place with three pointers.
* Best for frequent insert/remove; not ideal for fast random access.

---

See you next time!
