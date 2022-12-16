# Basics of Data Structures

I have been struggling to understand what data structures. I decided to take my time to dig into it and I would like to share the knowledge of basic concepts I gained.

**What is Data Structures?**

A single data item on its own it's gonna mean much, but if put together with a bunch of other data items then it becomes meaningful.
This data has to be stored in a structure, choosing the right one is important.
The way we measure how a data structure is by doing a specific item like; adding a new item; .add() .get() .sort() .search() is called **Big 0 notation** 
**Big 0 notation** is the measure of how well an operation scales.

**The basic Data Structures.**

**1. Linked lists.**

The atomic unit of a linked list is a node that contains a value and a pointer.
**A value** is a number; i.e 12.
**Pointer** connects you to the next node in the chain. thus the linked part of inked lists.
The first node in the list is known as the head while the last one, that doesn't have the next pointer is known as the tail.

**Pros and Cons of Linked lists**

Pros
- Good at adding new items 
- Good at deleting nodes because we can just change where the pointer is pointing.

Cons
- Not good at retrieval
-Not good at Searching, even when the index of the node is known, because each node is only aware of the node next to it.


**2. Array.**

This is a continuous block of cells in computer memory.
An array by keeping track of its memory location can constantly computer the location of any item inside it. 

**Pro**

- Good at searching,

**Con** 

-  Not good at adding items, because you have to move the array to a new place so that it fits(in a high-level language)
In low-level languages, you have to do the extra work of declaring the size of your array.

**3. Hash Table {}**

- **{}** is an object in Javascript and a dictionary in python.
The key  gets run through a function(hashing function) and it spins out the memory location. It's different in the way that the memory locations don't have to be next to each other.
When two keys hash to the same memory location depending on the hashing algorithm used, it is called a **collision**

**Pros**

- Good at adding or removing items

**Con**

- Key collisions.

**4. Stack + Queue**

This is mostly used for an algorithm called; Breadth - First - Search(BFS).

**Stack** - it operates in using a First in First Out algorithm; adding an item on the top(.push1), removing the last item(.pop())
Call stack tracks the functions that have been called. 
Stacks are important for an algorithm called Depth - First - Search(DFS). 

**Queue's** operate in a first in first out logic.

**5. Graphs + Trees**

**Graph;** similar to linked lists. Where nodes point to the other nodes. Except in this case the pointers are called **edges** and edges can have numbers assigned to them(**weights**).

**Trees;** they are a special kind of hierarchical graph in which the data extends out in the direction. Trees can be used to represent a lot of stuffs like, a family tree, HTML tree with nested elements. 

Binary Search Tree has  specific kind of rules, but this rules allows one to search effectively. 

**Big O Notation**

Big O Notation is used to measure the efficiency of an algorithm. There are two types; 

1. Time Com plexity
2. Space Complexity

**Grading time and space.** 

Every line of code has it's own time and space complexity. To get the time complexity quickly, simply ask;
 
- How does the input size i.e string length/ array length affect the specific line?
- Does the variab le scale with the size of the input?

This is article is meant to give a basic understanding of Data structures. This [here](https://www.youtube.com/watch?v=8hly31xKli0) is a free full course to help you understand Data Structures and Algorithms.

