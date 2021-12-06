# Midterm 2 Review

## Queue

Has two main operations `enqueue` and `dequeue`. It is a **first-in first-out** data structure. Think of it as a queue of people at an amusement park. We separated the deque operation into dequeue which removes the element and front which returns the first element but sometimes these are rolled in together.

### Linked List Implementation

We can represent the queue as a linked list as long as we have `tail` pointer that points to the last element in the list. To implement this, we pop elements from the head for dequeue and front operations and enqueue new elements after the tail pointer. 

### Array Implementation

We need to use a circular array to do this. This means creating a back pointer for the array which points to the first open index. If we hit the last element of the array, we wrap around to the front of the array and dynamically grow it when the back pointer equals the front pointer.

```java
int front = ++front % capacity; //allows us to increment the front pointer wrap around the array if needed.
```

We add new elements at the back pointer and dequeue by incrementing the front pointer. 

We will also need to dynamically grow the array. When front == back, we loop from front to back to copy the elements in order into the new array, set front to 0 and back to the number of elements + 1.

A **Steque** supports push, pop, and enqueue so pushing to both ends and removing from only one end. A **Quack** allows push, pop, and dequeue which is adding only to the top, but removing from the top or bottom. A **Deque** allows insertion and removal at either end in O(1) and allows you to implement Stack, Queue, Steque, and Quack by choosing which operations you use.

Practice implementing Deque operations

## Positional List

### Doubly Linked List

A linked list with nodes that track their next and previous nodes. Even with this, we still can't implement binary search because we cant jump to an $i^{th}$ element.

There are a lot of edge cases to consider when implementing a doubly-linked list. One way to fix this a little is to have sentinel nodes that are never revealed to the client. These are head and tail nodes that we insert between. This way, we never need to consider the case where we have null head or tail pointers.

We also need to expose the nodes to the client, but we don't to accept nodes from another list or allow the client to break the data structure. To do this, we create the 

```java
public interface Position<T> {
    T get(); // returns the data at a position, but this isn't even necessary. Need a generic class to return instead of node.
}
```

now that we have a `Position` interface we can implement the `Node` class:

```java
public static class Node<E> implements Position<E> {  //static gives outer class access to nested class variables.
    E data;
    Node<E> next;
    Node<E> prev;
    DoublyLinkedList<E> owner; //nodes track the memory address of their owner.
    
    Node(E data, DoublyLinkedList<E> owner) {
        this.data = data;
        this.next = null;
        this.prev = null;
        this.owner = owner;
    }
    
    @Override
    E get() {
        return data;
    }
}
```

With this `Node` class implementation, we can return `Position` objects to the client and check that the Node owner is the `DoublyLinkedList` that it came from.

Notably, when we want to downcast `Position` to `Node`, we need to manually do this. `Node<T> node = (Node<T> position);` which can throw `ClassCastException e` (and technically null pointer exception. We need to throw our own `PositionException` to tell the user that they messed up.

`node.owner != this` is how we test if the node doesn't belong to this instance of `DoublyLinkedList`.

```java
public class DoublyLinkedList<T> {
    private Node<T> head;
    private Node<T> tail;
    private int numElements;
    
    public DoublyLinkedList()  {
        head = null; //initialize to sentinel to avoid edge cases.
        tail = null; //initialize to sentinel to avoid edge cases.
        numElements = 0;        
    }
    
    public Position<T> addFirst(T t) { //no edge cases handled here.
        newNode = new Node(t, this);
        newNode.next = head;
        head.prev = newNode;
        newNode.prev = null;
        head = newNode;
    }
    
    public Position<T> addLast(T t) { //no edge cases handled here.
        newNode = new Node(T, this);
        newNode.next = null;
        tail.next = newNode;
        newNode.prev = tail;
        tail = newNode;
    }
    
    public Position<T> get(int idx) { //no edge cases handled here.
        Node<T> cursor = tail;
        for (int j = numElements - 1; j > idx; j--) {
            cursor = cursor.prev;
        }
        return cursor; //upcasting to position is handled automatically.
    }
    
    //helper method to convert a Position from the user to a Node if possible and if owned by this list.
    private Node<T> convert(Position<T> position) throws PositionException{
        try {
            Node<T> node = (Node<T>) position; //manually downcast to Node<T>
            if (node.owner != this) { //check list ownership
                throw new PositionException();
            }
        } catch (NullPointerException | ClassCastException e) {
            throw new PositionException();
        }
        return node;
    }
    
    public void delete(Position<T> target) {
        Node<T> target = convert(target);
        target.prev.next = target.next; //can throw null pointer exception without sentinels.
        target.next.prev = target.prev;
    }
    
    public Position<T> insertAfter(Position<T> target, T data) {
        Node<T> node = new Node<T>(data, this);
        Node<T> target = convert(target);
        node.next = target.next;
        target.next.prev = node;
        target.next = node;
        node.prev = target;
        return node;
    }
    
    public Position<T> insertBefore(Node<T> target, T data) {
        Node<T> node = new Node<T>(data, this);
        Node<T> target = convert(target);
        target.prev.next = node;
        node.prev = target.prev;
        node.next = target;
        target.prev = node;
        return node;
    }
}
```

### Positional List ADT

```java
public interface List<T> extends Iterable<T> {
    int length();
    boolean empty();
    Position<T> insertFront(T data);
    Position<T> insertBack(T data);
    Position<T> insertAfter(Position<T> p, T data) throws PositionException;
    Position<T> insertBefore(Position<T> p, T data) throws PositionException;
    void remove(Position <T> p) throws PositionException;
    void removeFront() throws EmptyException;
    void removeBack() throws EmptyException;
    Position<T> front() throws EmptyException;
    Position<T> back() throws EmptyException;
    boolean first(Position<T> p) throws EmptyException; //if position p is the first element in the list
    boolean last(Position<T> p) throws EmptyException;
    Position<T> next(Position<T> p) throws PositionException; //the next element in the list after p
    Position<T> previous(Position<T> p) throws PositionException;
    Iterator<T> forward();
    Iterator<T> backward();
}
```

using a doubly linked list, we can implement all of these operations in constant time. We make sure our DLL returns positions which enables `insertBefore` and `insertAfter` to work in constant time.

## Set

A set is an unordered collection of objects. We also define an ordered set which can only take inputs that extend `Comparable<T>` which allows us to sort them. 

```java
public interface Set<T> extends Iterable<T> {
    void insert(T t);
    void remove(T t);
    boolean has(T t);
    int size();
}
```

### Linked List Implementation of Set

We actually can't do better than $O(N)$ implementation for `has`, `insert`, and `remove` using either a singly or doubly linked list. This is because to run insert and remove, we need to know if the element is in the set which requires looping over all elements in the worst case. `has` similarly can only be implemented with linear search. Only `size` can be done in $O(1)$ because we can track `numElements`.

#### Move To Front Heuristic

This is a trick which says whenever we call `has` or `insert`, we move the element to the front of the list. Then the next time we call `has`, `insert`, or `remove` the item is found more quickly. If we work under the assumption that there is a subset of values in the set that we are interested in, these elements get moved to the front of the list and are easier to find the next time we search for them. These operations need to be sub-linear so that the heuristic actually improves runtime.

### Array Implementation of Set

`has` runs linear search on the array and finds if the element is in the set in $O(N)$. If the data is ordered, we could implement binary search, but sets aren't necessarily ordered so we can't really do this. `insert` appends the element to the end of the array and grows it if necessary. Needs to ensure the element is not already in the set so runs in amortized $O(N)$. `remove` also has to check if the element is in the list so also runs in $O(N)$.

#### Swap Heuristic

We can improve the performance of search over many iterations with an array implementation of a set by implementing this swap heuristic. We can't efficiently move a found element to the front of the array directly as we would have to move the element that was at the front backwards which would defeat the purpose of the heuristic with multiple elements in the subset we are searching for. However, we can just swap the found element with the element to its left. As we search for it over many searches it will "bubble up" to the front of the array along with other commonly searched for elements and will be found more quickly.

#### Fail-Fast Iterators

To implement the set iterator, we just loop from the  front of the set to the end of the set. 

When we implement an iterator, we don't want to allow the user to alter the set while we iterate over it. This could corrupt the order of iteration and cause us to iterate incorrectly especially in a randomly ordered data structure like a set. We need to track if we have modified the array while iterating. To do this, we could just have a boolean called `modified` that is initialized to false at the beginning of iteration and set to true if any modification functions are called. We then throw an exception and quit iteration.

#### Ordered Set

```java
public interface OrderedSet<T extends Comparable<T>> extends Set<T> {
}
```

The elements we put in the ordered set have a notion of order.  We now need to keep the nodes in the linked implementation sorted which cannot be done in better than $O(N)$ time complexity. We can now implement the array implementation of set with binary search to do the searching in $O(lg(N))$ but insertion and removal are still $O(N)$

## Binary Search Trees

A tree is composed of **nodes**. The first node in a tree is called the **root** node. A binary search tree is a branched data structure. Every node except for the root node has a **parent** and zero or more children (up to 2 in a BST). Nodes that do not have children are called **leaves**. **descendants** are all of the nodes that are children of a given node or children of those children and so on. **ancestors** are the opposite. **siblings** are nodes that share a parent.

### Binary Trees

A binary tree has at most two children for each node. Each child of the root is itself a binary tree called a **subtree**. Non-linear linked data structures as compared to linear data structures like linked lists.

### Binary Search Trees

Binary search trees are a subclass of binary trees that ensures the tree and its subtrees follow an ordering property. Namely, every value to the left of a given node is less in value to that node and every node to the right is larger than the node.

```java
public class BSTOrderedSet<T extends Comparable<T>> implements OrderedSet<T> {
    private Node<T>  root;
    
    private static class Node<E> {
        E data;
        Node<E> left;
        Node<E> right;
        Node(E data) {
            this.data = data;
        }
    }
    
    private boolean has(T val, Node<T> node) {
        if (node == null) {
            return false;
        }
        if (val == node.data) {
            return true;
        } else if (val > node.data) {
            return has(val, node.right);
        } else {
            return has(val, node.left);
        }    
    }
    
    public void insert(T t) {
        root = insert(t, root);
        numElements++;
    }
    
    private Node<T> insert(T t, Node<T> node) {
        if (node == null) {
            return new Node<>(t); //add a new value where null was.
        }
        
        if (t > node.data) {
            return insert(t, node.right);
        } else if (t < node.data) {
            return insert(t, node.left);
        }
        
        return node; //if the value is aready in the data structure, don't do anything.
    }
    
    public void remove(T t) {
        root = remove(t, root);
        numElements--;
    }
    
    private Node<T> remove(T t, Node<T> node) {
        if (node == null) {
            return node; //don't do anything to the tree as the value isn't in the tree
        }
        
        if (t > node.data) {
            return remove(t, node.right);
        } else if (t < node.data) {
            return remove(t, node.left);
        }
        
        return remove(node); //the node.data == t so remove it.
    }
    
    private Node<T> remove(Node<T> node) {
        //handle node has one or no children
        if (node.left == null) {
            return node.right;
        } else if (node.right == null) {
        	return node.left;    
        }
        
        //node has two children so swap value with in-order successor (max valu in left subtree)
        Node<T> successor = max(node.left);
        T temp = successor.data;
        successor.data = node.data;
        node.data = temp;
        
        node.left = remove(successor.data, node.left); //remove the swapped element from the left subtree.
        return node;
    }
    
    //find rightmost node in left subtree
    private Node<T> max(Node<T> node) {
        if (node.right == null) {
            return node;
        }
        return max(node.right);
    }
    
}
```

To check if a node is in the binary search tree, we traverse the appropriate subtrees. For example if the value is less than the value at the root,  we search the left subtree for the value if it's greater than the node at the root, we search the right subtree. Once we reach a leaf we conclude the value is not in the data structure. This is easy to implement recursively. See above.

To insert a node, we first check if it is in the data structure with `has` or if we want to save on iterations, repeat the search process and once we get to a node that has a null child where we want to insert our value, we create a new node and insert it at the appropriate position. 

To remove a node, we similarly traverse the tree looking for it, then we  have three cases to consider. The first case is when  the node is a leaf. If the node is a leaf, we can just point the parent to null where this node is. When the node is inside the tree with exactly one child, we can point its parent to its child to extract it. Finally, when the node has children, to remove it, we need to find its **in-order successor**. This is the node that comes immediately before this node in a list of nodes sorted by value. This means we need to find the largest value in the left subtree or the smallest value in the right subtree. It is helpful to have a separate helper function to find this successor node. To perform the removal, we can swap the value at the node to be removed with the value at its successor and call remove on former successor node which is easy since it is now a leaf.

### Tree Traversal Terminology

#### Level Order Traversal

This says go over the tree level by level. Start at the root and print every node to the left and right. Then go to the nodes you printed and print their direct children. Then repeat until there are no more children to print. This prints a representation of the tree.

```java
public void levelOrderTraversal(BinarySearchTree<T> root) {
    Queue<T> q;
    q.enqueue(root);
    boolean levelHasChildren = root != null;
    while(!q.isEmpty() && levelhasChildren) {
        levelHasChildren = false;
        int levelSize = q.size();
        while(levelSize > 0) {
            if (hasChildren(q)) {
                levelHasChildren = true;
            }
            levelSize--;
        }
    }
}

private hasChildren(Queue<T> q) {
    Node<T> node = q.remove();
    if (node != null) {
        System.out.println(node.data);
        Node<T> rC = node.right;
        Node<T> lC = node.left;
        q.add(lC);
        q.add(rC);
        return rC != null || lC != null;      
    } else {
        q.add(null);
        q.add(null);
        //System.out.println("null");
        return false;
    }
}
```

#### In-Order Traversal

This prints the elements of the list in order. Easier to implement with recursion. First we visit everything to the left of the node first, print the node, then print the things to the right. The heuristic for this is **Left, Root, Right**

```java
public void inOrder(node) {
    if (node == null) {
        return;
    }
    inOrder(node.left);
    print(node);
    inOrder(node.right);
}
```

#### Pre-Order Traversal

This prints the root first, then the left, then the right element. This makes sure that the root prefixes its children. Heuristic for this is **Root, Left, Right**

```java
public void preOrder(node) {
    if (node == null) {
        return;
    }
    print(node);
    preOrder(node.left);
    preOrder(node.right);
}
```

#### Post-Order Traversal

This prints the left subtree, the right subtree, then the root. The heuristic for this is **Left, Right, Root**

```java
public void postOrder(node) {
    if (node == null) {
        return;
    }
    postOrder(node.left);
    postOrder(node.right);
    print(node);
}
```

#### More Terminology

**Path** is a sequence of nodes through a tree where each node is connected. There are k-1 connections if there are k nodes. It is the edges between nodes from the first node to the last nodee.

**Length** the length of a path is k-1 where k is the number of nodes in the path. The number of connections or edges between nodes.

**Height** the height of a node is the <u>length of the longest path from the node to a leaf</u>. The height of the root node defines the height of the tree.

```java
public int height(Node<T> n) {
    if (isLeaf(n)) {
        return n;
    } else {
        return 1 + Math.max(n.left, n.height);
    }
}
```

**Depth** the depth of a node is the opposite of its height. **Level** is another word for depth. The height of the tree is the depth of its deepest node. Length of the path from the root to the node.

A **Perfect Binary Tree** is one in which every node has exactly two children and all of its leaves have the same depth (level). In a perfect tree, the number of nodes is $2^d$ where d is the depth of the node. The total number of nodes $n = 2^{h+1} - 1$ is found by summing all the values of 2 where $h$ is the height of the tree. We can solve for the height of the tree (depth of the deepest node) with the following formula derived from the earlier equation $d = lg(n + 1) - 1$. Therefore, the height of a perfect binary tree is $O(lg(n))$.

#### BST Analysis

The worst-case efficiency of a binary search tree is $O(h)$ where h is the height of the tree. This is absolute worst case when the nodes are inserted in order as we form a linear linked list rather than a tree of length N which takes $O(N)$ time to search. The best case scenario is when the BST is a perfect binary tree. The height of an n-node binary tree is $O(lg(n))$ as we saw above so it will take this many steps to insert, remove, or find an element. We want our tree to be as shallow as possible to have the best performance.

A general tree has an unlimited number of child nodes:

```java
public interface Tree<T> extends Iterable<T> {
    int size();
    boolean empty();
    Position<T> insertRoot(T t) throws InsertionException;
    boolean root(Position<T> p) throws PositionException;
    Position<T> root() throws EmptyException;
    Position<T> insertChild(Position<T> p, T t) throws PositionException;
    boolean leaf(Position<T> p) throws PositionException;
    Position<T> parent(Position<T> p) throws PositionException;
    T remove(Position<T> p) throws PositionException, RemovalException;
    Iterator<T> iterator();
    Iterable<Position<T>> children(Position<T> p) throws PositionException'
}
```

## Maps and Balanced Binary Search Trees

### Map ADT

A `Map` is a collection of key-value pairs. The keys must be **unique** and **immutable**. Maps are also known as dictionaries or associative arrays. The core operations of a map are the insertion, removal, and update of its key-value pairs and lookup of a value stored at a given key. The Abstract Data type is summarized below:

```java
public interface Map<K, V> extends Iterable<K> {
    //Insert a new key-value pair. Exception if k is null or already mapped.
    void insert(K k, V v) throws IllegalArgumentException;
    //removes the key-value pair from the map and returns the value associated with the key
    V remove(K k) throws IllegalArgumentException;
    //Update value at a key, exception if k is null or unmapped.
    void put(K k, V v) throws IllegalArgumentException;
    //return the value at a key, throw exception if null key or unmapped key
    V get(K k) throws IllegalArgumentException;
    boolean has(K k); //check the existence of a key.
    int size(); //number of mappings.
}
```

### Balanced Binary Search Tree

As we saw above, we want the our BSTs to be as close to perfect binary trees as possible for maximum efficiency. This means we need to balance our trees as we add elements.

We define a new  subclass of binary tree called the BBST which has all of the properties of a BST with the added a balance property that says the heights of a nodes left and right subtrees are either equal or differ by at least 1. If this property is violated, the tree is a BST and not a BBST.

We can programmatically define balancing with **Balance Factors** which are tracked by each node in the tree which tracks the height of the left subtree minus the height of the right subtree:

```java
bf(node) = height(node.left) - height(node.right);

public int height(node) {
    if (node == null) {
        return -1; //ensures that leaves have BF = 0
    } else if (isLeaf(node)) {
        return 0;
    } else {
        return 1 + Math.max(height(node.left), height(node.right));
    }
}
```

A BBST is balanced if for every node in the tree, the balance factor is 1, 0, or -1.

## AVL Trees

This gives us a technique for maintaining a BBST as we insert and remove new items. Ensures that every operation performed in these trees is optimally $O(lg(N))$ where N is the number of elements in the tree.

The operations we implement need to be $O(lg(N))$ or better as there is no point in using an AVL tree if its going to harm the performance of the BST to worse than what it would be default.

There are 4 main patterns that we observe and resolve differently as directed by the algorithm.

#### Structural Rotation

Any unbalanced BST can be converted to a BBST by applying structural rotation. Both insertion and removal can cause the tree to become unbalanced so we need to apply these to correct it after applying the function. 

* **Single Right Rotation:** We need to apply this rotation when the problem is in the **left subtree of the left child from the perspective of the unbalanced parent node**. To implement single right rotation, we promote the root of the left subtree to become the new parent node, move its right node to become the left subtree of the parent node, and demote the parent node to become the left subtree of the promoted subtree root.

  * ```java
    Node<T> rightRotation(node<T> root) {
        Node<T> leftChild = root.left;
        root.left = leftChild.right;
        leftChild.right = root;
        root = leftChild;
        return root;
    }
    ```

* **Single Left Rotation:** The opposite problem to that which caused singleRightRotation. Here, the problem is in the **right child in the right subtree**.

* **Right-Left Rotation:** Occurs when the problem is in the **right child's left subtree**. A right-left rotation is applying a right rotation to the left subtree which creates a linear chain that can be resolved with a left rotation. 

* **Left-Right Rotation:** Occurs when the problem is in the **left child's right subtree** from the perspective of the parent node. We need to apply a left rotation to the right subtree to promote it, then a right rotation to balance the parent. 

A positive balance factor indicates that the subtree is **left-heavy** while a negative balance factor indicates that the subtree is **right-heavy**. Overall, a parent balance factor of -2 tells us to look at the right subtree of that parent and a child's balance factor of -1 indicates that we need to look at the right subtree of the child node which means the imbalance can be resolved with a **left rotation**. A parent balance factor of -2 with a child balance  factor of 1 indicates that the child is left heavy while the parent is right heavy so we need to apply a **Right-Left rotation**. A parent balance factor of 2 tells us to look at the left subtree of the parent and a right heavy child indicates we need to apply as **left-right rotation**. A parent bf=2 with child balance factor of 1 indicates both the parent and child are left heavy and we need to apply a **right rotation**.

Insertion can only imbalance one node at a time, while removal can require up to $lg(N)$ rotations all the way up to the root.

## Priority Queue

Recall a Queue is FIFO. A priority queue works by taking elements of higher priority over elements that may be inserted earlier in the queue. Each item has a priority that is either assigned or based on its natural ordering. The highest priority (can be lowest value or highest value depending on implementation) element gets returned first no matter what.

### Comparator vs Comparable

To redefine the natural ordering of programmer-defined objects, the object needs to implement the `Comparable` interface to have a defined natural ordering. This means the `compareTo()` method is overridden with a new definition. If we had an array list of custom objects that are comparable, Java will be able to sort them based on the fact that they are comparable.

If we want to make a different way to compare these objects other than the natural ordering, such as by another parameter in the class, we can provide a `Comparator` object in Java to functions like `Collections.sort(arrayListOfObjects, new customComparatorClass())`. This tells the sort function to sort based on the overridden `compare()` function within the `customComparatorClass`.

```java
private static class CustomComparatorClass implements Comparator<Submission> {
    @Override
    public int compare(Submission s1, Submission s2) {
        return s1.getNumPriorSubmissions() - s2.getNumPriorSubmissions();
    }
}
```

which will sort the  user-defined submission class based on the number of prior submissions variable it contains rather than whatever the natural ordering is.

Remember both `compare` and `compareTo` work by returning 0 when both objects are equal. They return a value > 0 when the first value is greater than the second value and a value < 0 when the first object is less than the second one.

When defining our priority queue, we provide a default constructor which uses the natural order of the types in the queue and a second constructor which takes in a `Comparator` which can be used to give the elements different priorities.

### Implementation

Regardless of the underlying data structure, we can find the next element to dequeue in $O(1)$ time if we keep the array sorted. 

To implement the priority queue with an array, we keep the best element at the end of the array and remove it by decrementing numElements. Insertion will be $O(N)$ since we need to find the element to insertAfter and copy over the elements after this.

To implement the priority queue with a linked list, we can keep the best element at the head and the next best attached to the head. We just have to removeHead to remove the element. To insert into the sorted linked list, we still have to iterate over all of the elements to find the element to insertAfter and we cant apply binary search on a linked or doubly-linked list.

The best priority queue is thus, one that uses a tree and can find, add, and remove elements in $O(lg(N))$ time.

### Binary Heap

A tree-based priority queue. A heap is a **complete binary tree** which is a new subclass of binary tree that limits its height to $O(lg(N))$ and requires that the priority of a parent node must be better than or equal to the priorities of its children. The next element to return is thus, always the root since it has the highest priority.

**A complete binary tree** is one where the tree is "full" on all levels except possibly the last level which must have all of its nodes on the left side. This is a slightly looser condition than the perfect binary tree since not all of the leaves have to be on the same level. A tree is a complete binary tree if when you ignore the lowest layer of leaves, the remaining layers are a perfect binary tree. 

The ordering of the BST is value of left child is less than parent which is less than right child. In a heap, the children have priority no better than the parent and the actual values at the nodes don't matter.

**Heap Order** The binary heap is either ordered as a **min-heap** in which the value of each node is less than or equal to the value of its children with the minimum value element at the root. Or **max-heap** in which the root has the highest value priority and the children of each node have a lower value priority than their parent.

A binary heap is NOT a BST so the nodes don't get sorted by their value. They get inserted according to their priorities.

### Array Implementation of Binary Heap

There is a trick to implement a binary heap as an array rather than an actual tree. For convenience the 0th index never gets a value. The $K^{th}$ element of the array has its left child at the index $2K$ and the right child is at the index $2K+1$. The parent of the $K^{th}$ element in the array is at the index $K/2$. 

To implement the `best` function, we just return the value at the root (K = 1). To implement `insert`, we have to new element  at the next leaf slot from the left. To do this, we add the new element to the end of the array and then correct the heap ordering property. To do this, we swap the child with its parent until the inserted element's children are of lower priority than itself and it is of lower priority than its parent. The value thus "swims up" the tree which occurs at most from leaf to root which is of height $O(ln(N))$. `remove` is always done from the root so we just swap the value for removal with the last element of the array and decrementing numElements. Now we have a value at the root that likely violates ordering so, we allow it to sink down by jumping through the children until ordering is restored. When implementing sinking down, we always pick the child to promote that has the highest priority. This ensures ordering is maintained.

## Treap

Essentially a heap that is implemented as a BST. Rather than using the natural ordering of the elements, we randomly generate a priority for the element when we insert it. It is very unlikely to get a linear natural order by randomly generating priorities for larger numbers of randomly inserted elements. The height of the treap is thus probabilistically likely to be $O(lg(N))$. 

To maintain the order of the treap (min or max-heap), we need left and right structural rotations. A right rotation promotes a left subtree root to be the root of the current subtree and a left rotation promotes a right subtree root to be the root of the current subtree. 

Unlike the priority queue, treaps are BSTs so the natural ordering of the elements is still considered in the Treap. The value at the left child must be less than the parent and the right child greater than the parent. The heap aspect of the treap means that the parent has higher priority than any of its children. 

We need structural rotations as described earlier to maintain the BST ordering and the priority ordering. 

## Hash Tables

BSTs allow us to implement sets and maps in logarithmic time, but Hash Tables let us perform these operations in (amortized) constant time!

The core of this is that we have some constant time **hash function** that converts a key to an index in the hash table which can be done in constant time. The hash function performs two main operations **generating a hash code** and mapping the hash code to a smaller range that can be used in the hash table called **compression**. The first is usually left up to the implementation of the objects we store in the hash table while the second is handled by the hash table data structure.

A good hash function is:

* <u>Uniform:</u> which means it maps keys to indices as evenly as possible. Want an equal likelihood of generating each index value. A non-uniform hash function is biased.
* <u>Deterministic:</u> is the core of the operations of the hash table. Every time we insert the same key, we get the same index out for a given size table. Otherwise our implementation breaks down.
* <u>Cheap:</u> the function needs to run quickly. Even if the time it takes isn't dependent on the size of the data structure, it still needs to be simple and fast to compute.

the faster and more uniform the hash function is, the more performant the hash table is. 

### Generating Hash Codes

The java Object class has a `hashCode` method which does this for you. User-defined classes need to override this or else the hash code is defined based on their memory address which doesn't allow identical objects to hash to the same value. We don't do this because hashing is complicated.

### Compression

To map the hash code to the index range of our data structure we can use the following snippet:

```java
int index = key.hashCode() % M; //where M is the size of the hash table.
```

Smaller values of M are more likely to experience collisions. A **collision** is when two different keys map to the same index. For practical implementations, the number of possible keys is much larger than the size of the array so collisions are unavoidable.

### Handling Index Collisions

There are two main collision handling techniques:

#### Open Addressing

In this technique, when a key maps to an index that already holds a value, we stick the value in the next available open index.

**Probing** is the word for the different techniques we can use to locate the next open location.

**Linear Probing** is when we just move to the next open index in the list.

```java
int index = getIndex(key);
//if table[index] is occupied:
for (int i = 0; i < M; i++) {
    index = (getIndex(key) + i) % M; //where M is the size of the hash table (num indices).
    //break loop when we find an open index.
}
//if we don't find an open index, the table is full (shouldn't get here due to load factor (see later))
```

If our find operation gives up when it reaches an open index without finding the element its searching for, removing elements from the hash  table will break our implementation. To fix this, we need to use **tombstones** which allow `Entry` objects in the hash table to track whether they are deleted (class variable to hold isDeleted boolean). The problem with this is that tombstones take up space in the data structure. If we remove a lot of elements, most of the data structure gets filled with junk and the more likely our find operation will run in $O(N)$ time. We generally don't overwrite tombstones as this requires tracking where they are to fully search for an item already being in the table which adds complexity.

**Contamination** describes this problem of tombstones taking up too much space in the hash table. We solve this problem by **rehashing** which is a process in which we create a new table of larger size and re-hash the entries in the old table for insertion in the new table (the index changes since the modulo changes with new size). We do not copy over tombstones.

**Load Factor ($\alpha$)**: allow us to quantify how full the table is. For linear hashing, the load factor is just:
$$
\alpha = \frac {number\ of \ filled\ cells} {table\ capacity}
$$
we trigger rehashing when the load factor exceeds a predefined value. Trying to maintain a lower load factor means we deal with larger hash tables and thus, use more memory.

**Prime Number Table Sizing:** When we rehash the table, we should multiplicatively scale the size the table but simply doubling the size of the table isn't the best way to do it. The best thing to do is to choose the smallest prime number larger than twice the current table size. Using prime numbers minimizes the number of ways that a key K hashes to the same index in a hash table of size M. Every key K that shares a given common factor with M will be hashed to the same value. By choosing M to be prime, we minimize collisions.

We implement this by having a pregenerated list of the first many prime numbers and just use doubling for numbers that exceed this. The data structure tracks which prime was last used and just increments to the next size on rehashing. If the size of the table exceeds the largest prime in the list we can just double as performance increases from the prime number probably wont make much of a difference.

To quantify the average-case performance of linear probing, we can use the following relationship that the expected number of probes in an unsuccessful search is:
$$
O(\frac{1}{1 - \alpha})
$$
which is extracted from probabilistic analysis beyond our scope. Different alpha choices thus affect the performance of the table as expected.

##### Primary Clustering

When the probability of the next element getting inserted after a large cluster increases with the size of the cluster as a result of the implementation of linear probing. Quadratic probing allows us to jump indices using constant size stride increases. This still creates clusters

Instead of the earlier probing implementation, we use the following implementation:

```java
for(int i = 0; i < M; i++) {
    index = (getIndex(key) + i*i) % M;
```

this takes larger strides by we can skip indices entirely depending on the size of the table. This can cause us to fail to insert or trigger resizing when the table isn't completely full (imagine there are open slots, but the jumping falls into a cycle such that it always misses the open spots). However, using low load factors and prime number table sizes prevent this. We still get clusters forming but this is secondary clustering and is better distributed throughout the table.

##### Double Hashing

When instead of variable step sizes, the step size is determined by another hash function. This means keys that collide with eachother will search for open spots differently and decreases the likelihood of clustering. 

Choosing to  implement other probing techniques really doesn't improve performance that much. Its more of an academic research thing. Linear probing is fine for most applications.

#### Chaining

In chaining, we store index collisions in an auxiliary data structure like a linked list. Each position in the hash table stores multiple entries if necessary. This approach is also called bucket hashing. 

We can just addFront a new element to the linked list after verifying its not already in it.

In the best case, the number of elements inserted is smaller than the capacity of the table and unique indices were generated for each key. In this case the hash table operations are $O(1)$ since we don't have to search for the value. In the worst case all elements hashed to the same index so we have a singly-linked list and insert, remove, and find are all done in linear time.

A uniform hash function should evenly distribute elements amongst indices so each bucket is expected to be of size $\alpha = n/M$ where n is the number of items stored in the hash table and M is the size of the hash table. We define this as our load factor $\alpha$ for chained hash tables. If we keep $\alpha$ < 1, we get an expected constant runtime operation. 