# CS 1332 Study Guide
Author: Oliver Zheng
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

### Binary Trees: 
- Has the following properties:
  1. Each node has at most two children (Left & Right).
  2. Children of a node are an ordered pair. 
- Order pair explained: 
  1.	The tree A can be represented as: (A(B(D()())(E(H()())(I()()))) (C(F()())(G()())))
      ![Order](https://github.com/ZhengQY421/CS-1332-Study-Guide/blob/master/Pictur2e.png?raw=true)
  2.	An empty tree is (). 
  3.	Each non-empty tree/substree is: (value left right)
-	Arithmetic Expression Tree:
    1. Internal nodes: operators 
    2. External nodes: operands 
    3. InOrder Traversal (LRootR)
    4. Example: (2 × (a - 1) + (3 × b))
    ![A](https://github.com/ZhengQY421/CS-1332-Study-Guide/blob/master/Picture1.png?raw=true)

- Notations
  - n = number of nodes
  - e = number of external nodes
  - i = number of internal nodes
  
- Properties
  - e = i+1
  - e = i+1		
  - e < 2h				
  - h < (n-1)/2
  - n = 2e-1		
  - h > log2
  - h < i			
  - h > log2 (n + 1) - 1
  
- Shapes:
  1.	Complete - all levels, except the last, are full, and the leaves are filled left to right. 
  2.	Full - every node, except the leaves, has two children.
  3.	Balanced - the height of each node's left and right subtrees can only differ by 1. 

## VII. Binary Search Tree (BST)
- Left child < Node < Right Child
- InOrder traversal traverses tree in ascending order!
- Performance:
  - Spaced used is O(n)
  - Add, search, and remove take O(logn) in best case and O(n) in worst case. 
- Operations: 
  1. Searching:
     1. Check node data
        - If greater than toSearch, go left
        - If less than toSearch, go right
        - If equal, data found 
     2. Repeat until found or reaches a leaf, which means not found. 
  2. Adding:
     1. Same as search
     2.	Repeat until found or if reaches a leaf, add as a child of the leaf. 
  3. Removing:
     1.	If has no children, simply remove it
     2. If one child, the child replaces the node to be removed 
     3. If two children, either the predecessor or the successor replaces the node to be removed.
        -	Predecessor - the largest node in the left (< current) subtree
        -	Successor - the smallest node in the right (> current) subtree. 
## VIII. AVL Trees
- Designed to resolve issues of BST having average of O(log n) for operations. 
- All AVL trees are balanced BSTs, but not BSTs are AVL trees. 
- Searching operation remains the same.
- Adding & Removing
  - After a node is added/removed, the heights and balance factor of the added/removed node are updated, and if necessary, rotations are done. Implemented recursively. 
  1. Balance factor (bf) - Calculated by subtracting the height of the left subtree by the height of the right subtree. 
     1. 0 = Perfect balance.
     2.	-1/1 = considered balance but slightly heavier on right/left side. No rotations can be done to make tree balanced. 
     3.	Other values mean that subtree is unbalanced and at least one rotation needs to be done.
  2. Rotation Types:
     1. Left Rotation: A node with a bf of -2, and its right child has a bf of 0 or -1. 
     ![LR](https://github.com/ZhengQY421/CS-1332-Study-Guide/blob/master/PictureLR.png?raw=true)
     2.	Right Rotation: A node with a bf of 2, and left child has a bf of 0 or 1. 
     ![RR](https://github.com/ZhengQY421/CS-1332-Study-Guide/blob/master/PictureRR.png?raw=true)
     3.	Left-Right Rotation: a node with a bf of 2, and left child has a bf of -1. 
     ![LRR](https://github.com/ZhengQY421/CS-1332-Study-Guide/blob/master/LRR.png?raw=true)
     4.	Right-Left Rotation: A node with a bf of -2, and right child has a bf of 1.
     ![RLR](https://github.com/ZhengQY421/CS-1332-Study-Guide/blob/master/RLR.png?raw=true)
- Performance: 
  1. Amoretized and worst case are all O(logn).
## IX. B-Trees (2-4 Trees)
- Similar to BST & AVL in that smaller items are on the left while larger items on the right. 
- Each node can have multiple items. 
- **Order** of a B-tree is how many items and possible children each node has. 
  - 2-4 trees have an order of 4
### 2-4 Trees
- Each node can have 3 items and up to 4 children. 
- Data items in each node are sorted in ascending order. 
- Children sorting order:
  - First child < First item
  - First item < Second child < Second item
  - Second item < Third Child < Third item 
  - Third item < Fourth Child
- Example:
  ![24Ex](https://github.com/ZhengQY421/CS-1332-Study-Guide/blob/master/Screen%20Shot%202018-03-06%20at%2000.18.07.png?raw=true)
- Properties:
  - Depth of all leaf nodes are the same
  - If there are n data items in a node, there are either 0 or n+1 children
  - Always balanced. 
- Performance: 
  - Search, Add, Remove are worst case O(log n). 
- Operations:
  1. Searching
     1. Starting from root, compare first data with toSearch
        - toSearch < Data: Go to nth child, where n is the position of data compared to in node (ie. 1st, 2nd)
        - toSearch = Data: Found
        - toSearch > Data: Go to next data in node
        - Go to last child if toSearch is greater than all.
     2. Repeat until found or go off the tree (data doesn't exist in tree). 
  2. Adding
     - Always added as a leaf node
     - Follow same steps as search until data is located or not found.
        - If not found, add data as a leaf node. 
        - If found, implement what is defined by the data structure writer. 
     - Overflow
        - After a data is added to a leaf node, the node may have more than 3 items. 
        - To solve this, the 2nd or 3rd item (middle item) is promoted to parent node (creates one if none), and current node is split into two nodes. 
          - Smaller items become promoted item's left child.
          - Larger items become promoted item's right child.
  3. Removing
     1. Follow same steps as search until data is located or not found. 
     2. Once found, remove the data
     3. Then depending on the circumstances: 
        1. Nothing if current node has no child and has at least one item. 
        2. If the current node is empty and has child nodes, then move the predecessor/successor into the node. If predecessor/successor is now empty, continue fixing depending on circumstances:
           1. If any of the empty node's sibling have more than one data, then rotate that data to fill the empty node (similar to AVL).
           2. If all of the empty node's siblings have only one data, then bring down a reasonable data item from parent and merge with left/riight sibling. Repeat one the two options if this results in an empty/invalid parent node. 
     - [Operation Examples](CS-1332-Study-Guide/B-Trees%20Examples.pdf)
## X. Heaps
- Heaps are used when there is a need to keep a set of items in ascending/descending order but want to avoid O(n) worst case operation performance as that of a traditional list. 
- Commonly represented as a binary tree and called a maxheap/minheap, where the root is the largest/smallest item. Can also be represented as an array. 
### Properties
1. **Order Property** - Parent node is always larger than children. No relationship between children. 
2. **Shape Property** - A heap is always complete, which means each level of the tree is always filled except for the last level, which must be filled left to right without gaps. 
3. Only root may be accessed, which means heaps *cannot* be searched through. 

### Array Implementation:
- Root is always at index 1 (0 makes math more challenging). 
- Given an index i
  - left child would be at 2i
  - right child wouldbe at 2i+1
- Parent of an index i would be at i/2
- Operations:
  1. Adding:
     1. Add the new item to the next open slot in the heap
     2. Compare the item to parent, and swap parent and child if order property is broken (heapify, usually recursive). 
     3. Repeat until reached root or there is no need for a swap. 
  2. Removing: 
     - Can only remove from root. 
     1. Remove from root 
     2. Move item in heap's last slot to the root. 
     3. Compare and swap the item with the smaller/larger child depending on if it's a minheap/maxheap. 
     4. Repeat until there is no need for swap or you reach the bottom of the heap. 
- Performance: 
  - Adding in amoretized and worst cases are both O(logn). Best case is O(1).
  - Removing is O(logn).
### BuildHeap 
- Algorithm used to covnert an array of numbers into a heap. 
- Assuming there is a variable called size for the array:
  ```
    Iterate index from size/2 to 1:
        heapify(index)
  ```
- O(n) performance 
- [Example](docs/BuildHeapExample.pdf)
### Priority Queue
- A data structure that, depending on implementation, return the items in ascending/descending order. 
- Used for printer jobs, CPU schedulers, etc. 
- Efficiently implemented using a heap. 
## XI. Maps
-	A collection of key-value entries. Each key maps to a value. 
-	Maps uses integer keys as indices in the range of [0,N-1] where N is the capacity of the Map.
### Hash Map
-	Hash Map is a data structure that is similar to a map, but hash code of the key is used to determine its key index. 
-	Hash Map performance in ideal case is O(1), and in worst case is O(n). 
-	Hash Codes can often exceed the range of the HashMap, so calculations need to be performed to reduce the hash code value to an acceptable index in the HashMap. 
  - Hash Code % array.length = valid index. 
- HashMaps uses load factor to determine when the hash map backing array should be resized (new size is usually 2n+1)
  - load factor = (number of key-value pairs)/(array.length)
  - When resizing, each index of each key-value pair needs to be recalculated. 
- A collision occurs when the hash code calculations of two key-value pairs yield the same value.
  - Also, two different objects may have the same hash code as indicated by the hash code contract. This means two different objects types will have to occupy the same space. 
- **Collision Handling #1** - External Chaining
  1. Essentially a linked list is implemented at each index.
  2. Collided key-value pair is added into the linked list. 
  3. When searching, first determine the key index, and then search the linked list for the key. 
  4. When removing, search the key and remove the key-valued pair from the linked list.
- **Collision Handling #2** - Linear Probing :(
  1. If there is a collision, then index i+1 is checked to see if empty. If not i+2 is checked, then i+3, and so on and so forth (go to the start of the array if reached the end). Inserts at the empty slot. 
  2. When searching, determine the key index, and continue check the next index if the key is not found at the current index. 
  3. Stop when the key is found, the entire array is traversed, or an index has NULL. 
  4. When removing, search the key and set that index to NULL. 
      - This would break the search if the key was moved due to collision. To solve this, set a "deleted" marker that indicates something was once stored. However, this also means that adding becomes more complicated because the key to add may be a collided key may already exist elsewhere in the array. To solve this, if came across an index marked "deleted," save the index. Add to the saved index only if the key is not found in the hash map.
- **Collision Handling #3** - Quadratic Probing
  1. Same as linear probing but instead of checking i, i+1, i+2, i+3, you instead check i, i+12, i+22, i+32….
  2. Collisions are more spaced out and other key-value pairs may not be shifted too much from their ideal index. 
  3. However, not all empty slots are checked and a key-value pair may not be added in. In such case, the backing array will need to be resized when you have probed n = array.length times. 
- **Collision Handling #4** - Double Hashing
  1. Uses a secondary hash function and places in the first available cell in the series beginning from the index calculated by the second hash function. 
  2. Secondary hash function cannot have zero values. 
  3. Common secondary hash function: *q-k mod q* where q is the hash code.
## XII. Skip List
- Linkedlist searching is O(n), but this can be improved by having randomly chosen items in another list and have the act as a "marker." This reduces search time by searching fewer items. 
- A skip list is similar to a linked list with items in ascending order, but a skip list has multiple levels. Each level has ideally half of the items of the level before it, so first level would have all items, second level has half of the items, etc. 
- A random coin flipper is used to determine if an item gets promoted and how many times it is promoted when adding. 
  - Heads: Item is promoted to the next level. 
  - TailsL Item is not promoted and no more flips are done. 
- Skip List Node (Quad-Node):
  - A reference to the item stored.
  - References to previous and next nodes in that level. 
  - References to node directly connected in the previous/next level. 
  - The level the node is on. 
- Phantom Nodes
  - Nodes used as a starting and/or ending marker. Not necessary in most data structures.
  - A negative infinity starting node is necessary at each level, a positive infinity ending node is optional at each level. 
- Operations:
  1. Searching
     1. Start at the top left phantom node
     2. Check data in right node
        - toSearch < data: toSearch doesn't exist on current level, move down one level. 
        - toSearch > data: go to the right node
        - toSearch = data: data found
     3. Repeat until data is found or go off the list (data not found). 
  2. Adding
     1. Used the coin flipper to determine the highest level the data will be on. Data is added to the highest level and every level below the highest level. 
        - ie. 3 heads were flipped before the first tail, the highest level to add data is 3. 
     2. Create as many new levels as needed if the max level is higher than the current amount of levels. 
     3. Traverse the skip list same as search, but add the item to the current level if need to. 
     4. Repeat until reach the bottom level
     - Note that handling duplicate items is implementation defined. 
  3. Removing 
     1. Traverse the skip list same as search, but at each level, disconnect the node from the rest of the nodes on that level and remove any empty levels. 
     2. Repeat until reach the bottom of the list. 
- Performance:
  - Best Case: All operations are O(logn)
  - Amoretized: All operations are O(logn)
  - Worst Case: All operations are O(n) --> All items on the same list
  - Space Complexity in the worst case is O(nlogn) but amoretized is O(n). 
  
## XIII. Sorting
- **In-Place Sort** is a sorting algorithm that doesn't copy over elements into another array/list, so a fixed amount of space is used. 
- **Stable Sort**  is a sort in which the order of duplicate items is preserved. For example, if the unsorted list has two instances of "Pikachu," then in the sortefd list, the first "Pikachu" will come before the second "Pikachu."

### Bubble Sort
- Starting at the beginning of the array each time, swap an element with its next element if out of order. Then move on to the next elment. Continue to do so until the end of the array is reached. The biggest element of the iteration is now at the end of the array. Repeat but excluding previous sorted items. The most recent sorted item is always treated as the "end of the array" of an iteration. 
- Performance: 
  - Best case is O(n)
  - Worst case is O(n^2)
  - Average case is O(n^2)
- In-place and Stable.
- Steps: 
  1. Compare items 1 & 2, if they are not in order, swap them. 
  2. Proceed items 2 & 3, if they are not in order, swap them. 
  3. Repeat until the end of the array, which is one iteration. The last item is in its correct position. 
  4. Repeat steps 1-3 but excluding the last sorted item and with the next two items. Continue until the array is sorted. Note that if no swaps were made during an iteration, the array is sorted.
  
### Cocktail Shaker Sort
- A variation of Bubble Sort. What is different is that for each iteration, the direction of traversal and the type of element to sort alternates. In the first iteration, the array is traversed from *left to right* and the at the end, the largest element of that iteration is sorted to the end of the array. In the second iteration, the array is traversed from *right to left*, beginning at the element before the sorted element from that last iteration, and at the end, the smallest element of the iteration is at the beginning of the array. Everything else is same as Bubble Sort. 
- Performance:
  - Best case is O(n)
  - Worst case is O(n^2)
  - Average case is O(n^2)
  
### Insertion Sort
- The array will have a sorted and unsorted portion. In each iteration, an element from the unsorted portion is taken and swapped with elements in the sorted portion until it's postioned correctly in the sorted portion. 
- Insertion sort always has a fixed number of iterations. 
- In-place and Stable.
- Performance:
  - Best case is O(n)
  - Worst case is O(n^2)
  - Average case is O(n^2)
- Steps:
  1. Assume the first item is sorted.
  2. With the next item, compare it with the previous item and swap until it's in the correct position (item before is samller). 
  3. Repeat step 2 until the entire array is traversed. 
  
### Selection Sort
- In each iteration, search the array for the smallest item and swap it with the element at the beginning of the array. Repeat until the array is sorted. The beginning of the array is always treated as the next element of the last sorted element. 
- In-place, **not** Stable. 
- Performance:
  - All cases is O(n^2)
- Steps:
  1. Mark the first element as the smallest item.
  2. Traverse the array to find the smallest item and mark it.
  3. Swap that item with the first element. 
  4. Repeat but excluding the sorted items. 
  
### Divide and Conquer Sorts
- Recursive. 
- Advantage in that portions of the sorting algorithms can be done in parallel (multiple threads). 

### Merge Sort
- Divide and Conquer
- **Not** in place, but Stable
- Performance:
  - Worst case is O(nlogn)
  - Best case O(nlogn)
- Steps:
  1. Divide the array into 2 equal parts, one part containing the left half and the other the right half. 
  2. Cotinue dividing the previously divided parts until each part only has one element. Now each part is sorted
  3. Merge the two parts together, starting from the part of the only one element. 
     - Have two markers of the elements to add back into the merged array for both parts. 
     1. Take the smaller of the two parts and add that that to the merged array. 
     2. Move the marker to the next element.
     3. Repeat until all elements in both parts have been added to the merged array. 
     - Note if all elements of one part has been added, no comparisons need to be made and the other part can just be added.
  4. Repeat for the larger divided parts.
  
### Quick Sort
- Divide and Conquer
- In-place but **not** Stable
- Performance:
  - Best case is O(nlogn)
  - Worst case is O(n^2)
- Steps:
  1. Choose an element at random to be the pivot
  2. Swap the pivot with the first item
  3. Set a left marker that starts with the second element, and a right marker that starts at the last item. 
  4. Move the left marker to the right as long as it is smaller than the pivot and doesn't cross the right marker.
  5. Move the right marker to the left as long as it is bigger than the pivot and doesn't cross the left marker. 
  6. If left and right didn't cross yet after the move, swap the two and move each one left/right by one element. 
  7. The right marker should now be to the left of the left marker. 
  8. Swap the pivot with the right marker, which is the correct position the pivot should be at in the sorted array. 
  9. Perform quick sort to the elements to the left and right of the pivot. Repeat until array is sorted. 

### Quick Select
- **Not** a sort. 
- Finds the kth smallest element in an array. 
  - For example, in [5,3,2,1,4], the k = 4 th smallest element is 4. 
- After quick select is performed on an array, everything less than the kth element is on its left side, while everything larger than the kth element is on its right side. Note that the left and right section will not be sorted. 
- Performance:
  - Best case is O(n)
  - Worst case is O(n^2)
- Steps:
  1. Choose an element at random to be the pivot
  2. Perform quick sort steps 2-8 
  3. Check if the index of the pivot is the k
  4a. If not, and k is less than pivot index, perform quickSelect again on the section to left of pivot and vice-versa. 
  4b. If so, the kth element is found, and the quickSelect is now complete. 
  
### LSD Radix Sort
- For integers/numbers only 
- **Not** in-place, but Stable
- Runs a fixed number of iterations each time, depending on the length of the longest number. For example, 1000 would yield 4 iterations.
- Performance: 
  - Depends on the number of items in the array (n) and the length of the longest number (k)
  - All cases are O(kn)
- Steps:
  - Create 19 buckets, and each bucket is a queue. Buckets 0 - 8 repesent negative digits -9 to -1, buckets 9 is the 0 digit, and buckets 10 - 18 are positive digits 1 to 9. 
  1. For each iteration, take the least significant digit of each number (beginning with the ones digit). For example, 5 is the LSD of 45 in the first iteration. 
  2. Use that digit to calculate the appropriate index. 
  3. Add the number reperesented by that digit to the bucket at that index. 
  4. After all numbers have been added, remove all numbers one at a time starting from bucket 0 and add each number to the array starting at index 0. 
  5. Repeat for the rest of the iterations. At each iteration, the LSD is the next most significant digit (the tenth digit after the iteration of the ones digit). 
  
## XIV. String Pattern Searching Algorithms
- Note that the text being searched from is denoted *t*, with a length of *n*. The text to search fro is denoted *p*, with a length of *m*
- Efficiecny is evaluated at the number of comparisons each algorithm makes. 
### Brute Force
- Most inefficient and simple
- Steps
  1. Align p at the beginning of t
  2. Compare first character of p & t
  3a. If matches, compare the next character. 
  3b. If doesn't match, shift p to the right by one character of t and restart the comparison. 
  4. Once a match is found, align p with the next character of t (shift p to the right by one), and repeat to find more matches. If any character of p exceeds the last character of t, the search is over. 
- Performance:
  - Searching for the first match 
    - Best Case: O(m) 
    - Other Cases: O(mn)
  - Searching for all matches 
    - All cases: O(mn)
    
### Boyer-Moore
- Utilizes a last table to determine how much to shift p by upon mismatches. 
- The algorithm begins by comparing the last character of p.
- **Last Table**
  - A mapping from each character of the pattern to the last index index it appears in the pattern. 
  - All other characters not in the pattern is mapped to -1. 
  - Example: the last table of "dog"
  ![lt](https://github.com/ZhengQY421/CS-1332-Study-Guide/blob/master/ltEx.png?raw=true)
- Steps:
  1. Construct the last table using p.
  2. Align p with the beginning of t. 
  3. Compare the last charcter of p with its corresponding character in t. 
     - If matches, move to the previous character and continue comparision
     - If doesn't match:
       1. Take the character in **t** and find its index in the last table, called i.
       2. Aligh p so the character at i aligns with the mismatched character in t. 
          - If this causes p to be shifted towards the left, insteaf of applying this shift, shift p to the right by one character.
          - If i is -1, then shift p to the right by m, so the first character of p aligns with the character after the character aligned with the last character in p before the shift
       3. Restart step 3
  4. Once a match is found, shift p to the right by one character, and repeat step 3 to find more matches. If any character of p exceeds the last character of t, the search is over. 
- Performance:
  - Searching for the first match 
    - Best Case: O(m) 
    - Worst Case: O(mn)
    - Average Case: O(m + n)
  - Searching for all matches 
    - Best & Average Case: O(m + n)
    - Worst Case: O(mn)
    
### Knuth-Morris-Pratt (KMP)
- Utilizes a failure table to determine how much to shift p by upon mismatches. 
- **Failure Table**
  - a table of length m
  - Each entry represents a number representing the length of the longest suffix that's also a prefix up to that index. 
  - Sounds complicated, but the way to construct this table in code is simple:
    1. Creare two markers called i & j. i points to the frist character in p, while j points to the second character in p.
    2. Set the first entry in the failure table to be 0
    3. Compare characters pointed to by i & j
       - If the same, failureTable[j] equals i+1. Then move i & j forward by one character. 
       - If different, and i != 0, set i to failureTable[i-1]; j is unchanged. If i = 0, then failureTable[j] = 0, and move j forward by one character; i is unchanged. 
    4. Repeat step 3 until j reaches m. 
- Steps:
  1. Construct a failure table using p.
  2. Align p with the beginning of t
  3. Compare first character in p with t
     - If matches, move to the next character in p and t and continue comparison.
     - If doesn't match:
       - Mismatch is at the first character of p: shift p to the right by one and restart step 3. 
       - Mistmatch is not at the first character of p: 
         1. Assume mismatch occurred at index j of p. 
         2. Align index failureTable[j-1] of p with the mismatched character in t.
         3. Continue the comparison from index failureTable[j-1] of p. 
  4. Once a match is found, align index failureTable[m-1] of p with the letter after the last letter in t of the preivous match.
     - Example: ![MoreKMP](https://github.com/ZhengQY421/CS-1332-Study-Guide/blob/master/MoreKMP.png?raw=true)
  5. Repeat step 3 except begin comparison at the letter at index failureTable[m-1] of p to find more matches. If any character of p exceeds the last character of t, the search is over. 
- Performance:
  - Searching for the first match 
    - Best Case: O(m) 
    - Average and Worst Case: O(m+n)
  - Searching for all matches 
    - All cases: O(m + n)
  
## XV. Comparable & Comparator
### Comparable
- a native Java interface that uses compareTo() to allow two objects to be compared. 
  1. Contains only the compareTo(Object o) method
     1. Needs to be implemented. Define the way to compare the objects of the class implementing Comparable Interface. 
     2. One object will call compareTo() on another object. 
### Comparator
- a native Java interface that uses compare() to compare two objects. 
  1. Provides a reference for the Collections.sort (Collections e, Comparator c) method. 
  2. Write own Comparator class so unique comparator objects can be made. 
     1. Define compare(Object a, Object b) method in the class.
     2.	Compare will then take in two object parameters and compare them. 
### Example
```Java
 public class HDTV implements Comparable <HDTV> {
    private int size; 
    private String brand;
       
    public HDTV(int size, String brand) {
        this.size = size; 
        this.brand = brand;
    }

    public int getSize() {
        return size; 
    }

    public String getBrand(){
        return brand;
    }

    //...//

    public int compareTo(HDTV tv) {

        if (this.getSize() > tv.getSize)
            return 1;
        else if (this.getSize() < tv.getSize)
            return -1;
        else
            return 0; 

    }

public class SizeComparator implements Compartor<HDTV> { 

    public int compare(HDTV tv1, HDTV tv2) {
        int tv1Size = tv1.getSize(); 
        int tv2Size = tv2.getSize();

        if (tv1Size > tv2Size)
            return 1; 
        else if (tv1Size < tv2Size)
            return -1;
        else 
            return 0      
    }
  
}

public class Main {

    public static void main (String [] args) {

        HDTV tv1 = new HDTV(55, "Samsung");
        HDTV tv2 = new HDRV(60, "Sony");
        HDTV tv3 = new HDRV(42, "Panasonic");

        ArrayList<HDTV> a = new ArrayList<> ();
        a.add(tv1);
        a.add(tv2);
        a.add(tv3);

        Collections.sort(a,new SizeComparator());
        for (HDTV tv:a) {
            System.out.println(tv.getBrand()); 
        }
    }
}      
```
## XVI. Dynamic Programming
- An algorithm paradigm that solves a complex problem by breaking it down into a collection of simpler recurrent subproblems. Does not mean that we have to use recursion. 
- Bottom-Up Approach:
  1. Identify smaller/simpler subproblems
  2. Order of solving subproblems
  3. Solve subproblems before larger problem. 
### Longest Common Subsequence (LCS) Algorithm
- Find the longest common subsequence of two strings, A and B. 
- A subsequence is defined as a set of characters that is contained in both strings in the same order
  - Ex. LCS for ABCDE and AFUCE is ACE 
- Utilizes dynamic programming and a 2-D array, denoted L. 
  - L's row length is equal to the length of A, and its column length is equal to the length of B. 
- Have markers x and y track the index of each character in A and B, respectively. 
#### Steps:
1. Fill the first row and column of L with 0's 
2. Compare A[x] and B[y], if they
   - equal: fill L[x+1][y+1] with L[x][y]+1
   - do not equal: fill L[x+1][y+1] with Max(L[x][y+1], L[x+1][y])
3. Increment x by 1.
4. Repeat Steps 2 until x reaches the end 
5. Increment y by 1, Set x to 0. 
6. Repeat Steps 2-5 until y reaches the end
7. The value at L[A.length()][B.length()] is the length of LCS
- Note that HB's slides allow -1 as an index for L, so for L, all the x+1 and y+1 above would be replaced with x and y, while the x and y would be replaced with x-1 and y-1, respectively. 
#### Finding the LCS
1. Set x and y to A.length() and B.length(), reespectively. 
2. Have an array, denoted LCS, that reperesents each character of the LCS with each index. Have i represnet the index of LCS and set that to L[x][y]
3. Compare A[x-1] and B[x-1]
   1. if they equal, LCS[i-1] = A[x-1]. i--, x--, y--. 
   2. if they do not equal, comapre L[x-1][y] and L[x][y-1], 
      - if the first is bigger, x--.
      - if the second is bigger, y--. 
4. Repeat steps 3 until x or y reaches 0. 
5. LCS array should now represent the LCS. 

## XVII. Graphs 
- A graph is a set of nodes/vertices and a collection edges that connect each pair of vertices. 
- **Order**: Number of vertices. 
- **Size**: Number of edges. 
- **Degree**: Number of edges incident to a vertex. If all degrees equal, then the graph has that degree. 
- **Path**: A set of edges connecting two nodes. A simple path has no repeated verticies. 
### Clarification: 
- Graphs can have unconnected verticies
- Graphs can be directed, where all the edges flow in one direction 
- Graphs can be undirected, where all the edges flow in both directions. 
- Graphs can be weighted, where there are weight/cost associated with each edge. 
- A directed edge is an ordered pair of vertices (u,v), where u is the origin and v is the destination. 
- An undirected edge is an unordered pair of verticies (u,v). 
- A self-loop is an edge that connects a vertex to itself. 
- Two edges are parallel if they connect the same pair of vertices. 
- Two connected vertices are adjacent to one another and the edge is incident on both verticies. 
- A cycle is a path whose first and last vertices are the same. Simple cycle is a cycle of simple path. 
- The length of a path or a cycle is its number of edges. 
### Search Algorithm:
#### Depth First Search (Stack-based)
- Keep tracks of visited vertex.
- Recursive - each iteration is stored on the system stack. The iteration is popped once it is finished. 
- Starting from a vertex, for each of its unvisited neighbor, visit it and store it as visited. 
#### Breadth First Search (Queue-based) 
- Keep tracks of visited vertex. 
- Stores all the vetices to visit into a queue. 
- Starting from a vertex, visit it and add all of its neighbors to the to visit queue. Contintue the visit until to visit is empty. 
### Dijkstra's Shortest Path Algorithm:
- Finds the shorted path for weighted directional graphs from a starting to vertex to all other vertices. 
- Uses BFS to move forward. 
- Stores the distance in a map where each key is each vertex and points to the shortest path's weight. 
- Keeps track of visited vertices. 
#### Steps:
1. In the map to return, point each vertex (key) to a value of infinity distance.
2. Starting from a vertex, visit it and mark it visited. 
3. For each of the vertex's unvisitef neighbor s, add the neighbor to the toVisit list and check in the map if the current weight is greater than the sum of the weight to reach the vertex and the weight of the edge connecting to the neighbor. If so, update with the lesser weight. 
4. Repeat 2 and 3 until all vertices have been visited or there are no more vertices to visit. 
### Minimum Spanning Tree (MST)
- A set of edges that connects all vertices in a graph with the minimum total weight.
- Edges must not form cycles. 
- Only for weighted graphs.
- An MST has |V|-1 edges. 
### Prim's Algorithm for finding MST
- Starting from a vertex, find the minimum spanning tree by adding each of the smallest neighbor and repeating the process with the neighbor.  
- Utilizes a priority queue to find the smallest edge each iteration.
#### Steps
1. Start from a vertex, mark it as visited and add all of its neighboring edges to the priority queue, denoted toVisit. 
2. Remove an edge from toVisit, and check if the destination vertex has been visited. 
3. If not, mark it as visited and add the edge to the MST set. 
4. Add all of the destination vertex's neighboring edges to toVisit. 
5. Repeat steps 2-4 until all vertices have been visited or toVisit is empty. 
6. The MST set should represent the MST. If not, the MST is invalid and cannot exist. 
### Kruskal's Algorithm for finding MST
- Utilizes Greedy Algorithm.
- Adds all edges to a priority queue, and remove the smallest edge every iteration until a valid MST is formed. 
- Utilizes a DisjointSet to ensure there are no cycles in MST.
#### Disjoint Set
- Consists of DisjointNodes, where each node has a parent. The parent's parent is itself. 
- Each element/vertex can only be in one Disjoint Set.
- An element can be in a Disjoint Set of itself, acting as the parent. 
- Two important methods:
  1. Find(T data)
     - Finds the parent/root of the Disjoint Set containing the data
  2. Union(DisjointNode one, DisjointNode two)
     - Combines the Disjoint Sets containing each node
#### Steps
- Add all the edges to a Priority Queue, denoted toVisit. 
- Creates a Disjoint Set of all Vertices, where each vertex is a DisjointSet of itself. 
1. Remove an edge from toVisit
2. Check if it has been visited and check (find) if the two vertices of the edge are within the same Disjoint Set. 
3. If not, add the edge to the MST set and combine (union) the two Disjoint Sets containing each vertex. 
4. Repeat steps 1-3 until all vertices have been visited or there are no more edges toVisit. 
5. The MST set should represent the MST. If not, the MST is invalid and cannot exist. 

## XVIII. Misc
-	An abstract data type (ADT) is an abstraction of a data structure. It specifies data stored, operations on data, and errors associated with operations. 
-	Amortized means time complexity over many consecutive iterations. For example resizing array when adding to Array List.   

## XVII. Performance Table
Data Structure |Search |Add   |Remove |Space Complexity 
--- | --- | --- | --- | ---
Array List  | O(n)  | O(n)  | O(n)  | O(n)
BST | O(logn) to O(n) | O(logn) to O(n) | O(logn) to O(n) |O(n)
AVL | O(logn) | O(logn) | O(logn) | O(n)
2-4 | O(logn) | O(logn) | O(logn) | O(n)
Heap | N/A | O(1) to (Amoretized) O(logn) | O(logn) |O(n)
Hash Map | O(1) to O(n)| O(1) to O(n)| O(1) to O(n)| O(n)
Skip List | O(logn) to O(n) | O(logn) to O(n) | O(logn) to O(n) |O(n) to O(nlogn)

Sorting Algorithm |Best Case |Average Case |Worst Case |Stable |In-Place
--- | --- | --- | --- | --- | --- 
Bubble Sort |O(n) |O(n^2) |O(n^2) |X |X
Cocktail Shaker |O(n) |O(n^2) |O(n^2) |X |X
Insertion Sort |O(n) |O(n^2) |O(n^2) |X |X 
Selection Sort |O(n^2) |O(n^2) |O(n^2) | |X 
Merge Sort |O(nlogn) |O(nlogn) |O(nlogn)|X |
Quick Sort |O(nlogn) |O(nlogn) |O(n^2) | |X
Quick Select |O(n) |O(n) |O(n^2) |  |
Radix Sort |O(kn) |O(kn) |O(kn) |X | 

String Pattern Searching Algorithm|Best Case |Average Case |Worst Case
--- | --- | --- | --- 
Brute Force |First: O(m) <br>All: O(mn) |First: O(mn) <br>All: O(mn) |First: O(mn) <br>All: O(mn)
Boyer-Moore |First: O(m) <br>All: O(m+n) |First: O(m+n) <br>All: O(m+n) |First: O(mn) <br>All: O(mn)
KMP |First: O(m) <br>All: O(m+n) |First: O(m+n) <br>All: O(m+n) |First: O(m+n) <br>All: O(m+n)
LCS |O(nm) |O(nm) |O(nm)

*V stands for number of vertices and E stands for number of edges*

Graph Algorithms| Time Complexity
--- | ---
BFS | O(V+E)
DFS | O(V+E)
Dijkstra | O((V+E)log(V))
Prims | O((V+E)log(V))
Kruskal | O((V+E)log(V))


