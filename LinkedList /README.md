## 🧠 Cornell Notes

📘 **Topic:** Linked Lists in Java <br>
📆 **Date:** 27-07-2025 <br>
👤 **Course/Source:** Java DSA Course

---

### ✨ Cues / Questions

**Intro & Structure**

* What is a linked list?
* How does it differ from an ArrayList?
* What is a node?
* What are head and tail?

**Append**

* What does append do?
* How is it implemented?

**Prepend**

* What does prepend do?
* How is prepend implemented?

**Remove Last**

* Why is removing last O(n)?
* How do we find the new tail?

**Remove First**

* How is it different from remove last?
* What happens when there's only one node?

**Get**

* How is get(index) implemented?
* What’s its time complexity?

**Set**

* How do we set a value at a given index?
* How does it reuse get?

**Insert**

* How is insertion at index handled?
* When do we reuse append/prepend?

**Remove (by index)**

* How is removal by index done?
* What edge cases must be handled?

**Reverse**

* How do we reverse a linked list in place?
* Why are temp/before/after needed?

---

### 📝 Notes

#### ✨ Intro to Linked Lists

* Linked list: a linear data structure with nodes.
* Each node stores a value and a pointer to the next node.
* Uses `head` and `tail` pointers.
* Nodes are **not contiguous in memory**.
* No direct indexing like arrays.

#### 🔹 Node Structure

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

#### 🔹 LinkedList Fields

```java
class LinkedList {
    private Node head;
    private Node tail;
    private int length;
}
```

---

### 🔹 Append

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

* Adds to end.
* O(1) time.

---

### 🔹 Prepend

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

* Adds to front.
* O(1) time.

---

### 🔹 Remove Last

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

* Traverse to 2nd last node.
* O(n) time.

---

### 🔹 Remove First

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

* O(1) time.

---

### 🔹 Get

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

* O(n) time.

---

### 🔹 Set

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

* Reuses `get()`.
* O(n) time.

---

### 🔹 Insert

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

* Handles start, end, middle insertions.
* O(n) for middle.

---

### 🔹 Remove (by Index)

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
* O(n) time.

---

### 🔹 Reverse

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

* In-place reversal.
* Uses `before`, `after`, and `temp` pointers.
* O(n) time.

---

### ✅ Summary

Linked Lists offer flexible, dynamic memory usage and are optimal for frequent insertion/removal at the start or middle. Unlike arrays, indexing is linear, but pointer-based manipulation makes prepending, appending, and reversing efficient when used correctly.
