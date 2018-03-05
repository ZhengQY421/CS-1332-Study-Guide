# CS 1332 Study Guide
## I. ArrayList
* ArrayList is typically used to store Objects (primitives as Wrapper Objects). Arrays are used to store primitives and objects. 
* Dynamically resizes when adding to a full ArrayList. Java's built-in ArrayList resizes the array backing structure to 1.5 of its original size. 
* Accessing element is O(1). 
* Inserting/Searching/Removing is O(n) with the exception of the last element, which is O(1). 
## II. Linked List
* LinkedList can be understood as a chain of nodes, where each node has its own data and connection to the neighboring nodes. 
* Head of LinkedList can be accessed in O(1). Tail can also be accessed in O(1) if a tail variable was implemented; O(n) if not. 
* Accessing and searching elsewhere is always O(n).   

### Singly
- Each node links to the next node
- Removing tail is inefficient because there's no direct access to previous and it would take O(n).

### Doubly
- Each node links to both the next node and the previous node. 
- Special header and trailer nodes are dummy nodes, which are nodes that do not contain any data. Header's next is always the first node, while trailer's previous is always the last node. 
- If no dummy nodes, the head's previous will point to null and the tail's next will point to null. 
- Removing from front and tail are O(1), elsewhere O(n). 

### Circular 
- The last node's next will always point to the first node. 
- Can be both singly or doubly linked. 
- Accessing nodes has the same O() as the link type (singly/doubly). 
- Singly: tail's next is always head. 
- Doubly: head's previous is always tail. Tail's next is always head.
## III. Iterators 
- Iterators allow data structures to be easily traversed. 
- The data structure usually implements an Iterable interface and writes an iterator as an inner/private class.
-	If a data structure class implements Iterable and returns a proper iterator(), it can be traversed using a for-each loop. 
-	Multiple versions of iterators can be implemented by a data structure. 

### Iterable interface
  - 1 required method to implement:
  -	iterator()
    - returns an instance of the Iterator interface the data structure implemented.
    
### Iterator Interface 
  - 3 methods to be implemented: 
    - hasNext()
    - next()
    - remove() (Not Required). 

### Performance: 
- Most of the time same performance as the data structure. 
-	A LinkedList iterator would have better performance since Linked List get() would be O(n^2) (n for getting item, repeated n2 times), while an iterator would be O(n) (1 for getting item, repeated n times). 

## IV. Stacks
-	**Activation stack:** JVM keeps track of the chain of active methods with a stack. When a method is called, JVM pushes onto the stack a frame of local variables, return value, and program counter. When a method ends, its frame is popped from the stack and control is passed to the method on top of the stack.
-	Space used on a stack is O(n), and each operation runs in O(1).
-	**Downsides:** Stacks are limited and can cause exceptions in a few cases.

## V. Queues 
-	Insertion are at the rear of the queue and removals are at the front. 
-	**Main operations:** enqueue, dequeue. Other: isEmpty(), peek(), size(). 
-	Each operation is O(1) , takes up O(n) space.

## VI. Trees
### Terminologies
1.	**Root:** the topmost node without the parent.
2.	**Internal node:** node with at least one child. 
3.	**Leaf/External node:** node without children. 
4.	**Ancestors:** parent, grandparent, great-granparent. 
5.	**Node Depth:** number of ancestors.
6.	**Height:** number of levels of children
7.	**Descendant:** child, grandchild, great-grandchild.

### Traversals
1. PreOrder: visit node first before descendants. Node - Left - Right 
2. PostOrder - visit descendant before node. Left-Right-Node
3. LevelOrder - visit each node on each level in left to right fashion

###. Binary Trees: 
- Has the following properties:
  1. Each node has at most two children (Left & Right).
  2. Children of a node are an ordered pair. 
- Order pair explained: 
  1.	The tree on the left can be represented as: (A(B(D()())(E(H()())(I()()))) (C(F()())(G()())))
  2.	An empty tree is (). 
  3.	Each non-empty tree/substree is: (value left right) 







