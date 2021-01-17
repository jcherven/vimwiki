# lists-and-linked-lists

In the last video, we discussed Arrays: fixed-size data structures that use an
index to reference their contents. Now, we're going to talk about various kinds
of lists, which are extensions to the Array concept. In short, a list is an
expandable array. You use a list more or less just like you would use an array,
but you don't need to worry about the structure filling up. In truth though, a
list is actually a structure built on top of an array. When the underlying
array is full, the list creates a new array that is larger, and copies its
contents over automatically. 

You'll recall that this operation is an O(n) procedure, because when the new
array is created, the old array needs to be iterated over one index at a time
to copy the contents into the new array. Now this is still true with lists, but
most implementations of a list try to save time over the long run – whenever
the list needs to grow, the size of the underlying array is increased more than
what is actually needed. In Java for example, lists double in size when they
outgrow their arrays. If I have a list with 4 items, and the underlying array
is only size 4, trying to add a 5th item to the list will cause the list to
double the size of the underlying array to 8 before adding my new item to the
fifth position – index 4. In other languages, the resizing factor may be more
than 2. 

By increasing the size so much at once, the number of times the list has to
increase in size is reduced. By doing this, we say that the insertion time is
amortized out. That is, as the list increases in size, the time spent copying
arrays over is less than the actual number of elements. While the worst-case
insertion time for a list is O(n) – just like in an Array – the amortized
insertion time is only O(1). Now, the math behind this explanation involves
some calculus, but we can break it down. 

If I have an arbitrarily large list of size x, and our resizing factor is 2 -
meaning the array doubles in size when it's full – then I can assume that my
list has doubled in size in the past. When it did so, the actual number of
elements that needed to be copied over was n/2, because x is the final size
after the doubling. Before that, it might have been doubled once before, and
the number of elements needed to be copied was n/4. Before that, it was doubled
with n/8 elements to copy. This goes on until we get back to the beginning:
when the list was only size 1, and it doubled to size 2, and so on. When we add
up all the time spent copying elements while doubling our array, we get n/2 +
n/4 + n/8 + … + 2 + 1, which is less than n and rapidly approaches 1 as n
increases. In fact, it's even less than logN, if you work it out. 

So a list can retrieve or change a value by index at O(1), just like an array.
Inserting an element has a worst-case time of O(n), but we can say it amortizes
to O(1) over time. Overall, lists can be pretty handy! 

But arrays and lists won't take us everywhere. Eventually, you'll need a data
structure that is expandable like a list, but doesn't need the memory adjacency
that an array gives. Or you need to guarantee that inserting or deleting an
element from your data structure is actually O(1). For these situations, you
want a Linked List. 

Rather than use an array behind the curtain, a linked list is a node data
structure. That is, every element it contains is wrapped in another structure
called a node. A node contains the original data value, but might also contain
some additional variables as well. In a linked list, a node holds the value of
the actual element, but it also has variables that contain the memory address
of the next or prior node in the sequence. These nodes in a linked list make a
chain then, that can be traveled in one or both directions. 

Because there's no underlying array, a linked list doesn't have an index.
Instead, you just know the first node in the list, called the head. If you want
to retrieve a value from the list, you check the head. If the head doesn't
contain the value you want, then you get the address of the next node from the
head, and check that one. If that node doesn't have the value you want, you get
the address of the next node, and check that one, and so on. 

We can see then that searching for an element in a linked list is O(n), because
we have to traverse multiple nodes to find what we're looking for. This is no
different than searching an array for a value without knowing the index it's
located at. But inserting or removing an element from the list is guaranteed to
be O(1). This is because you only ever need to perform 3 steps to insert: get
the address of the node that will come after your inserted node, set your new
node to point to that address, and then update the address of the previous
node's neighbor variable to point to your new node. Deleting is even easier –
just set the “next” address of the previous node to the address of the node
that comes after the one you're removing. Like adding or removing the links of
a chain. 

However, this is really only that fast if you're inserting or removing at the
head of a linked list, and the tail of a doubly-linked list. Inserting or
removing from somewhere in the middle of the list would first require searching
to that position, which makes the overall operation O(n). But at least there's
no copying array elements! 

For an example, let's say that you're given a singly-linked list. How would you
write an algorithm that removes all duplicate values from the linked list? For
this problem, let's say you're not allowed to create any kind of buffer to
memorize values you have already seen. Go ahead and pause here if you want to
work this out yourself. 

This one is a little tricky. Remember that each linked list node contains it's
own data, and also the memory address of the next node in the list. If there is
no next node, the value of that variable will be null. 

```
algorithm removeDuplicates is
  input: LinkedListNode head
  output: node
  
  let current = head
  let runner = null
  
  while (current != null)
    runner = current
    while (runner.next != null)
      if runner.next.data = current.data
        runner.next = runner.next.next;
      else
        runner = runner.next
```

The only input we need for this is the head of the linked list, which is a
node. This algorithm won't have any output, it just removes items from the list
that it's given. Because the list is singly-linked, we can only move forward
through the list's nodes, not backwards. Our solution will first need to create
a variable that refers to the current node. This will start as the head node,
but for each node we'll need to check every node that comes after the current
one to see if they have duplicate values. To do this, we'll use a runner. This
is a second variable that runs through the rest of the list repeatedly,
starting at whatever the current node is, and stopping at the last node. 

So while the current node is not the end of the list, we'll create a runner.
The runner starts at the same node as the current one. While that runner is not
at the end of the list, we'll check if the data of the node after the runner
matches the data at the current node. If it does, we remove that node by
linking the runner to the node that comes after the next one. That is, if the
runner is at node 1, it compares the data of node 2 to the data of node 1. If
the two data match, then node 3 is linked to node 1, cutting node 2 out of the
list. Otherwise, if there's no match, the runner is moved to the next node.
That loop will run until the runner is at the end of the list. When it ends,
the current node is moved to the next node in the list after the head, and the
process continues. 

When the algorithm finishes, The loop will have checked every node, and removed
every duplicate of each node that came after the first occurrence. This
algorithm iterates over the list once with the “current” pointer, but the
“runner” pointer also iterates over each node, each iteration containing one
less node than the one before it. This will run in O(n^2) time – a rather
complex algorithm, but the best we can do without being able to track what
numbers we've encountered as we iterate through. 

How do we know it's O(n^2)? Let's plot it out. Here I've drawn a sample linked
list with 4 nodes, like a chain. Beneath that, I've written out the number of
iterations the first loop will run – one for each node, so 4. For each
iteration, I'm going to check if the runner visited the corresponding node. In
the first iteration, the runner starts at the head, and checks the data of each
node after that, until the runner exits the list – when the runner is null.
Then on the next iteration, the current pointer will be at the second node, and
the runner visits that node and every one thereafter. This continues on, and we
notice that our checkboxes form the shape of a half-filled in square. We know
the area of a square is x^2, and half that is of course x^2/2. Our nested loops
therefore run O(n^2/2) times, but with Big-O notation we ignore coefficients,
so that simplifies to O(n^2). 

In practice, linked lists aren't used as much as other data structures. Plain
lists or arrays are better for just storing elements, and there are other data
structures that are just as fast at inserts and deletes, and faster at
searching. But linked lists still have their place, and you should understand
how to use them. 
