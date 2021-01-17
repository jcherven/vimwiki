# data-structures

Variables are a useful way to store your data, but they don’t do much in the
way of organization. 

Consider a situation where you are writing code that represents a person’s list
of contacts. You have a bunch of variables that represent phone numbers, but
what do you do when you need to perform some operation over all phone numbers?
What if you need every phone number in another part of your application - how
do you pass them all around?When programmers need to organize their data, they
use data structures. These are standardized patterns of code designed to
organize one or more variables. The most common structures are often integrated
directly into the programming language itself, but their simple and
standardized nature makes implementing them on your own pretty easy. 

Arrays are the most common data structure, and are built into the core of
almost every programming language. An array is a linear collection of variables
of uniform size, and in typed languages, uniform type. What does this mean?
Well, we have previously discussed a little bit about how memory addressing
works. Memory space is allocated in units of bytes, and each variable occupies
a certain number of bytes in memory. An array reserves a certain amount of
adjacent bytes in memory - enough to fit a predetermined number of variables.
For example, we might say we have an array named “myArray” of size 5 - it holds
5 variables, and these variables are stored next to each other in memory. This
guarantee makes searching through an array very fast, because at the lowest
level, the computer always knows where to look for the next variable, and it
never has to look far. The guarantee also allows arrays to allow access to
their contents by an index. If I want to access the third object in an array, I
can just say, “myArray” and in brackets, “two.” 

Why say two, if I want the third item? Array indices start counting at 0
instead of one. You’ll see that this tradition holds in almost every type of
indexed data structure, so it’s a good idea to memorize this fact. If you
remove an element from an array, the array will just be empty at that index,
until it is filled later. 

One shortcoming of arrays is that they must always be of a fixed length, and
that length can only be set once. This is because, by definition, an aray has
to reserve that memory. But what if you don’t care about memory adjacency, and
you want a collection that can grow or even shrink as needed? Well in that
case, you would use a List, sometimes called a Vector. These data structures
are sometimes baked directly into a language, but are more often instead
implemented as discrete structures. They are essentially wrappers around
arrays, and expose the ability to add or remove contents through functions.
Because they are wrappers for arrays, they can still access their contents by
an index. I know what you may be thinking - if a vector is a wrapper around an
array, how can it grow in size? Well, when a the array in a vector or list gets
full, it automatically creates a new array that is larger - often double the
size of the previous array - and copies the contents of the old array into the
new one. When an element is removed from a vector or a list, the elements after
the now-empty position are usually shifted down to close the gap. This helps
keeps these structure a little leaner, but these features are a tradeoff of
performance for flexibility. 

A stack is like an list, in that it’s a flexible collection of elements. But
stacks enforce a procedure for accessing their elements, which is
Last-In-First-Out, or LIFO. Think of a stack as a stack of pancakes. When you
want to add a new element - a new pancake - you place it on the top of the
stack. And when you want to eat a pancake, you take one back off the top of the
stack. A queue is a similar idea, but instead of adding new items to the top of
the collection, you add them to the bottom. This is just like a person getting
into a line - the person at the front of the line gets removed first, and the
newest person at the end of the line gets removed last. In other words,
First-In-First-Out. FIFO. Stacks are generally used when you want to enforce an
ordering of events. Consider writing code to render a 3D animation. You have
all of these components that you need to rotate or translate to a different
location, but they need to be done in a certain order. If you were animating a
model of a person jumping, and that model had three parts, can you imagine what
it would look like if you rendered the model transformations out of order?

Queues on the other hand are most often used for scheduling. When you want to
try to ensure that every element has an equal wait time before being removed
from the collection, you’d use a queue. This ensures that the elements that
have been waiting the longest get resolved next. 

A linked list is an odd duck.  They’re like a list in that they’re a linear
collection of elements… but they have no index, and aren’t a wrapper for an
array. Instead, a linked list is made up of several structures called nodes.
Each node is a wrapper for the actual variable or object you want to put in the
linked list, but each node also additionally knows the memory address of its
neighbors. In this way, the contents of a linked list do not have to be
adjacent in memory, and the size is only exactly what we need it to be. 

But there has to be a downside, right? Well, navigating to any particular
element requires searching through every element in the list prior to it, which
is more time consuming that just accessing an element by an index. Adding or
removing a new element first requires navigating to the location you are
inserting to or deleting from, and grabbing the references to the next and
prior nodes to stitch them together after removing an element. A linked list
can be singly or doubly linked, meaning each node is aware of one or both of
its neighbors respectively. 

The last type of data structure I want to cover is the map, sometimes called a
dictionary. A map is a collection of nodes structures like an array list, but
each node is not aware of any others. Instead, each node both wraps the actual
variable or object being stored in the map, and also contains a key value that
can be used to refer to the node in question directly. The nodes themselves my
be stored in an array or a list or some other collection, but a map has to be
able to return a node when the appropriate key is supplied. Wondering why
they’re sometimes called a dictionary? Because a dictionary works exactly the
same way - when you want to look up the definition of a word, you provide the
word itself as a key, and get the definition as a value. 

Data structures will be a commonly used tool when programming, and knowing the
right one for a job will be critical. Some structures are faster for adding or
removing values, others are more memory efficient. Most modern languages have
optimized and convenient implementations of these collections available for use
by default, but not every language has a default implementation for every data
structure. 

# lecture notes
Data Structures are useful in organizing data. 

## Arrays

Arrays are a very common data structure. Typically, arrays store sequential pieces of data near one another in memory and thus searching through arrays is a quick operation to perform. Arrays are fixed-length structures. 

Other structures exist to allow for convenience of adding/removing data.

## List/Vector

A list is like an array, but provides support for adding/removing elements via methods. Generally, a List/Vector is an implementation of an array behind the scenes.

## Stacks

Stacks are similar to Lists, but they enforce a procedure for accessing their elements. Conceptually, a stack is similar to a pile of pancakes. Adding an element is like adding a new pancake to the pile; it is place on the top. When you eat a pancake you typically start at the top. LIFO (Last-In, First-Out)A LIFO order specifies that the last element placed in the structure is the first one removed when removing elements one-by-one. This behavior resembles the metaphor of a pile of pancakes. 

## Queue

A Queue is like a stack but typically enforces a FIFO procedure for adding/removing elements. Conceptually, it is similar to a line of guests waiting to be served at a movie theater. FIFO (First-In, First-Out)A FIFO order specifies that the first  element placed in the structure is also the first one removed when deleting elements.

## LinkedList

A Linked List is linear like a list, but index of an array that grows and shrinks in size, it is composed of nodes. Each node keeps track of another node and this forms a link or chain of elements. Adding/Removing elements to the middle of a linked list is a slow process, because you have to search through several nodes (down the chain) until you find your point of inserting/deleting the node. 

A singly-linked list is a uni-directional link of nodes. Each node only knows about the node in front of it. 

A doubly-linked list is bi-directional. Each node knows about the node in front of it and behind it. 

## Maps/Dictionary

A map is a collection of key/value pairs. One node is considered a key and it points to another which is considered the value. Together they form a pair, similar to how a dictionary associates a word (key) to its definition (value). 
