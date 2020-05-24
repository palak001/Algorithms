# Heaps and Heap Sort Algorithm

It' is awesome that you decided to learn about Heap Sort! Great, I will try my level best to walk you through it step by step and heap by heap!

Heap sort is unlike any other sorting algorithm. It’s a very special technique wherein **we visualize our array as being a tree**. And the way we do that is pretty simple. But before diving right into it, Let’s understand what we actually mean by heap here.

## Heaps <a id="6fa4"></a>

Heaps are nothing, but Binary trees forced to follow some extra rules. And those rules being —

![Source: Internet](https://miro.medium.com/max/649/1*ZSF5coHeIasQJSO61j3O9g.png)

1. **The binary tree must be a Complete Binary Tree.** \(By Complete I mean, every level, except possibly the last, is completely filled, and all nodes are as far left as possible.\) **Note:** The second image is not a heap because 3 has a right child without having a left one, thus violating the line: ‘_All nodes are as left as possible’._
2. **And all tree nodes must satisfy Heap Property.** Heap property differ depending on whether we are dealing with MAX heap or MIN heap. _**MAX HEAP PROPERTY:**_ For __Any node, it’s value is greater than or equal to it’s both child’s node value. Similarly you can figure out the MIN HEAP PROPERTY. For heap sort, we will basically focus on MAX Heaps.

Now the big question is, _**What has an array got to do with a heap!?**_  
As already stated, we are going to visualize an array as a heap.

![From the book Introduction to algorithm by T H O M A S H. C O R M E N](https://miro.medium.com/max/3360/1*yiWJS3ShT5gp0iDIS-b8Gg.png)

A being the array, i being array index \(0 index is left unoccupied\)—

1. Root of the tree : A\[1\]  
2. Parent of an element i : A\[ceil\(i/2\)\]  
3. Left child of an element i : A\[2\*i\]  
4. Right child of an element i : A\[2\*i + 1\]

With above thing in mind, **we can imagine each element of an array as a node of a tree and can see those seemingly unrelated indexes linked to each other.**

Now we are ready to proceed to Heap Sort Algorithm.

## Heap Sort Algorithm <a id="df3c"></a>

Basically there are 3 main steps:

1. Convert the array into Max Heap.
2. Exchange the largest element\(at index 1\) with the last element and remove it from the heap.\(which is equivalent to decreasing the size of the array\)
3. Restore the Max Heap property again and repeat it till you are left with only one element in the heap.

So first, we need to convert our array into a heap.  
We already know how to imagine an array as a binary tree.  
\(Index 1 is root of the tree, index 2 being its left child and 3 being its right child. Index 4, being index 2 left child and 5 being its right child and so on…\).  
Our task now is to convert this binary tree into a Max heap.

The way this is achieved is by using 2 functions:

**BUILD\_MAX\_HEAP**: To produce max heap from an arbitrary array.  
**MAX\_HEAPIFY**: Corrects a single violation of the heap property in a sub-tree.  
Or in simple terms ‘_max heapify’_ an almost ‘_max heapifyied’_ tree.

_MAX\_HEAPIFY_ is applied only when_,  
**The sub-tree rooted in the left and right of index i, are also max heap.**  
\(Only root element, if any, is the one preventing the sub-tree from being fully ‘max-heapifyied’\)**.**_

BUILD\_MAX\_HEAP internally uses MAX\_HEAPIFY function.  
Here we follow bottom up approach.  
We start _heapifying_ small parts, which in turn helps in _heapifying_ larger parts.  
_**Note**: All leaf nodes by definition follows Max heap property!_

## Pseudo code for **MAX\_HEAPIFY** <a id="6647"></a>

![From the book Introduction to algorithm by T H O M A S H. C O R M E N](https://miro.medium.com/max/3241/1*io2rvCxKQAbmwVB2Y0ZyKg.png)

Here we are checking if the Root element is greater than or equal to both its left and right child, in which case that tree is a max heap\(We have already assumed both left and right side are max heap.\), else we swap and recursively call the function MAX\_HEAPIFY on the sub-tree.  
By the time it’s over, we have a ‘_max\_heapifyied’_ sub-tree.

## Pseudo code for **BUILD\_MAX\_HEAP** <a id="2d8f"></a>

![From the book Introduction to algorithm by T H O M A S H. C O R M E N](https://miro.medium.com/max/1988/1*Qx1AQz4CFO0vUlhve74ZHA.png)

### In a complete binary tree having n nodes, ceil\(n/2\) nodes are leaf node, thus they are already a max heap in itself! <a id="3788"></a>

So BUILD\_MAX\_HEAP function calls MAX\_HEAPIFY function on all the nodes indexed from i = floor\(n/2\) to i = 1\(non leafy nodes\).

By the time it’s over, we have given our simple array a nice creepy look!  
On the face of it, It hardly seems getting any nearer to sorting, But only we know that it literally is…

_It’s more like solving a Rubik cube, you keep on applying tricks over it, and it seems like it’s leading no where, but then all of a sudden, few more moves and it’s solved!_

Let’s play our last card!

## Pseudo code for **HEAP SORT** <a id="eeb4"></a>

![From the book Introduction to algorithm by T H O M A S H. C O R M E N](https://miro.medium.com/max/2053/1*iksIKDgdKt-SBtSNtbdwSA.png)

As we know, The largest element exist at the root of heap, we interchange root element \(i = 1\)\(we are not using i = 0 index of the array\) with the last element of the heap and then remove it from the heap\(i.e decrease heap size by 1\).  
Because of this interchange, We have slightly disturbed our heap, so we again call max\_heapify on the remaining tree\(remember we can call it, because except root node, all are in their right places\)and this continues till we reach the index 2. By this time we have a completely sorted our array.

Time complexity of Heap Sort: O\(n log n\)

For more details on this and other algorithm topics, Checkout this book —  
_**Introduction to algorithm by T H O M A S H. C O R M E N**_  


