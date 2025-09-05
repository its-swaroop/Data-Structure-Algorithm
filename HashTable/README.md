# 📘 Hash Tables in Java – Complete Chapter Notes


## 1. Introduction to Hash Tables

* A **Hash Table** stores data in **key-value pairs**.
* Key is hashed → converted into an **array index**.
* **Hash Function**:

  * **One-way**: cannot reverse to get the key.
  * **Deterministic**: same key always produces same index.
* **Collisions** occur when two keys map to the same index.

Example: Hardware Store Inventory

```
Key: "nails"  → Value: 1000  
Key: "tile"   → Value: 50
Key: "lumber" → Value: 30
```

---

## 2. Handling Collisions

Two main strategies:

1. **Separate Chaining** – each array index stores a **linked list** of nodes.
2. **Linear Probing** – search forward to find next empty index.

> We use **Separate Chaining** for simplicity and efficiency.

Example of separate chaining:

```
Index 2 → [ ("nails", 1000) → ("tile", 50) → null ]
```

---

## 3. Constructor & Node Setup

```java
class Node {
    String key;
    int value;
    Node next;

    Node(String key, int value) {
        this.key = key;
        this.value = value;
        this.next = null;
    }
}
```

### Hash Table Class:

```java
class HashTable {
    private Node[] dataMap;

    HashTable() {
        dataMap = new Node[7];  // use a prime number to reduce collisions
    }
}
```

---

## 4. Hash Method

Converts a string key → array index.

```java
private int hash(String key) {
    int hash = 0;
    char[] keyChars = key.toCharArray();
    for (char c : keyChars) {
        int asciiValue = c;
        hash = (hash + asciiValue * 23) % dataMap.length;
    }
    return hash;
}
```

* `% dataMap.length` keeps the result within valid index range.
* `23` is a multiplier to distribute keys evenly.

---

## 5. Set Method (Insert Data)

```java
public void set(String key, int value) {
    int index = hash(key);
    Node newNode = new Node(key, value);

    if (dataMap[index] == null) {
        dataMap[index] = newNode;
    } else {
        Node temp = dataMap[index];
        while (temp.next != null) {
            temp = temp.next;
        }
        temp.next = newNode;
    }
}
```

* **If empty** → directly insert new node.
* **If collision** → add to end of linked list at that index.
* **O(1)** average case.

---

## 6. Get Method (Retrieve Value) – *Focus Section*

Used to **find the value for a given key**.

```java
public int get(String key) {
    int index = hash(key);
    Node temp = dataMap[index];

    while (temp != null) {
        if (temp.key.equals(key)) {
            return temp.value;  // key found
        }
        temp = temp.next;
    }
    return 0;  // key not found
}
```

### How It Works:

1. Hash key → find index.
2. Traverse linked list at that index.
3. If key matches → return value.
4. If end is reached → return default (0 or null).

* **O(1)** average case.
* **O(n)** worst case if too many collisions.

---

## 7. Keys Method (Collect All Keys) – *Focus Section*

Returns a **list of all keys** stored in the hash table.

```java
public ArrayList<String> keys() {
    ArrayList<String> allKeys = new ArrayList<>();

    for (int i = 0; i < dataMap.length; i++) {
        Node temp = dataMap[i];
        while (temp != null) {
            allKeys.add(temp.key);
            temp = temp.next;
        }
    }
    return allKeys;
}
```

### Explanation:

* **Outer loop** → iterates through array indices.
* **Inner loop** → traverses linked list at each index.
* Collects every key into `ArrayList`.
* **O(n)** where n = number of keys.

---

## 8. Interview Question – Find Common Items Between Arrays – *Focus Section*

**Problem:**
Given two arrays, find **common elements** efficiently.

### Naive Solution – O(n²)

```java
for (int i = 0; i < arr1.length; i++) {
    for (int j = 0; j < arr2.length; j++) {
        if (arr1[i] == arr2[j]) {
            System.out.println(arr1[i]);
        }
    }
}
```

* Nested loops → inefficient for large datasets.

---

### Optimized Solution Using Hash Table – O(n)

1. Insert all items from `arr1` into a hash table.
2. Loop through `arr2`, check if each element exists in the hash table.

```java
public static void printCommonElements(int[] arr1, int[] arr2) {
    HashMap<Integer, Boolean> map = new HashMap<>();

    for (int value : arr1) {
        map.put(value, true);
    }

    for (int value : arr2) {
        if (map.containsKey(value)) {
            System.out.println(value);
        }
    }
}
```

**Time Complexity:**

* O(n) to insert first array.
* O(m) to search second array.
* Total = O(n + m), far better than O(n²).

---

## ✅ Summary

* **Hash Table** = array + hash function + linked lists for collisions.
* **Collisions** solved via separate chaining.
* **Set** → insert data efficiently.
* **Get** → retrieve value using key.
* **Keys** → return list of all keys.
* **Big-O:**

  * Average case: O(1) for set/get.
  * Worst case: O(n) if many collisions.
* **Practical Use Case:**

  * Solve problems like finding common elements between arrays quickly.

---

See you next time!
