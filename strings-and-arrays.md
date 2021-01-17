# strings-and-arrays

Now that we understand the basic ideas behind algorithms and their ratings,
it's time to discuss some of the data structures you can take advantage of to
improve your algorithms,or even make them work in the first place. And every
data structure discussion must start with the humble Array. The array is the
most basic data structure shared by every language in use today. To understand
it, you must first understand the idea of a variable, and how memory is used by
computer programs. 

A computer's memory is broken up into bytes – 8 bits, or binary digits.  8 bits
makes a byte, 1024 bytes makes a kilobyte, 1024 kilobytes makes a megabyte,
etc. Computer programs use variables in the same way a math equation does –
they're a store for a value of some kind, but the particular value can be
changed. Some languages separate those values into groups, like integers,
alphanumeric characters, or decimal numbers. This is called typing. Whether a
language has typed or untyped variables, a variable is given a fixed amount of
memory space that it is allowed to occupy. For example, in Java, an integer
variable is allowed 4 bytes – 32 bits – of memory. This has two effects: first,
the range of integer values that variable could store is limited to what can be
expressed with 32 binary digits; second, the amount of memory reserved is
always going to be 4 bytes, even if the actual value stored doesn't require
that much space. Every byte of memory has an address, which is where the
computer knows to look for a particular value. If a variable occupies more than
one byte, typically the computer will know to access the variable through the
address of the first byte reserved. If any other variables are created, the
computer knows to reserve memory after the initial address plus the number of
bytes reserved for the variable stored there. 

So now that you understand that a variable is reserved memory space used to
store values, I can tell you that an array is simply a series of reserved
memory spaces for a fixed number of variables. If I have an array of 5
integers, and each integer is reserved 4 bytes of memory, my array is a chain
of 20 reserved bytes of memory. I can place values into this array at any point
using an index. Array indices start at 0, and go up to the array's size, minus
one. So my size-5 array of integers is indexed from 0 to 4. Array indices are
always wrapped by brackets. 

This is because, under the hood, an array is accessed by the first memory
address reserved for the first index. Accessing the value in another index is
simply a matter of accessing the address at… the array's first address, plus
the desired index multiplied by the number of bytes reserved for each variable.
So if my array starts at address 2, and each integer is reserved 4 bytes, then
accessing array index 3 is as simple as accessing memory address 2 + (4 * 3),
or memory address 14. 

Array values are thus said to be memory adjacent, which makes accessing the
values of an array just about as fast as anything can possibly be. Because
finding the value stored in any index of an array simply requires a single
multiplication equation, we say that an accessing an array by index is done in
O(1) time. No matter how big the array is, accessing the value at any index
only requires one step. This also holds true for changing the value at any
index. On the other hand, by reserving blocks of adjacent memory at once when
the array is created, an array's size is fixed. The only way to increase the
size of an array is to create an entirely new array of adjacent reserved bytes,
and copy the values of the first array into the second. We have to do this,
because if our array reserves 4 bytes of memory in a row, and another variable
should occupy the 5th, our array can't expand smoothly. 

So expanding our array requires creating a new array – reserving memory is
always an O(1) task, as is deleting the old array once everything is copied
over. But copying each value will require iterating over the entire length of
the old array, which is an O(n) task.  So for an O(1 + N + 1) algorithm,
remember that we can just say it's an O(N) task. This also illustrates why it's
better to create an array of a size you know you need, rather than start small
and expand later. The former will be an O(1) operation, the latter is O(N)
every time you need to expand. 

That brings us to Strings. A string is a series of alphanumeric characters,
like a word or a sentence. In most languages, these are implemented as arrays
of characters, where each character is allowed a certain number of bytes for
its encoding. Some languages also require the last character of a string to be
a special invisible character, in case the string is shorter than the amount of
reserved space, which prevents garbage data from being accidentally interpreted
as part of the string. But because this is a language-specific trait, we're not
going to factor it into our algorithms. Now that we understand Strings and
arrays, let's look at a simple algorithm that uses these together. 

Let's write an algorithm that determines if a given String is a palindrome. A
palindrome is a series of characters that are the same when read forward or
backward, like “racecar”. Generally, you ignore spaces with palindromes, but
for simplicity we'll assume our input phrase has no spaces or special
characters. Go ahead and pause here if you want to work it out yourself before
I go over a solution. We won't be using a specific language to write this
algorithm, we'll just be showing some language-agnostic pseudo code. 

```
algorithm palindrome is
  input: string phrase
  output: true/false result
  
  let length = phrase.length
  let c = 0
  
  while (c <= length/2)
    if (phrase[c] != phrase[length - 1 - c])
      return false
    c = c + 1
    
  return true
```

We'll start by showing our inputs and outputs. For input, we work with a string
variable named “phrase”. For our output, we return a boolean value that will be
either “true” or “false”. To run this algorithm, we create two new variables:
“length” will be a value that stores the length of the input phrase, and “c”
will be a value that stores 0, at least initially. This will be our “counter”
or “cursor” variable, which refers to an index of the phrase string. Then we
use a loop to iterate over each character in the input phrase. However, we're
comparing the first character to the last character, the second character to
the second-from-last character, etc. We only need to iterate over half the
characters in the phrase string to determine if the phrase is a palindrome. So
we use a while-loop, which only runs while the condition in parenthesis is true
– in this case, while the value of c is less than or equal to half the length
of the input phrase. 

For every iteration of the loop, we check if the character
at index “c” is not equal to the character at index “length” minus one minus
“c”. Remember that the length of an array is one greater than the actual last
index, because the index numbering starts at 0. As “c” increments by 1 with
each loop iteration, the characters compared converge toward the center of the
input phrase. So, when we compare the two characters, if they're not equal then
we know the phrase cannot be a palindrome, and we return false. Returning a
value always ends the algorithm immediately, and most languages only allow you
to return one value. If the characters actually do match, the value of c is
incremented, and the loop continues. If every character in the first half of
the phrase matches every character in the second half in reverse order, the
word is a palindrome and the loop will exit when “c” is greater than half the
length of the phrase. When the loop exits this way, the word must be a
palindrome, and so the value “true” is returned. 

The act of creating variables, returning values, and checking conditions are
all O(1) operations – they're just a single step or statement. Each iteration
of a loop can also be said to be O(1). But our loop iterates over characters in
the input phrase, and the longer the input phrase is, the more loop iterations
our algorithm will have. At first glance, we could try saying this algorithm is
O(1 + 1 + n/2 + 1), where n is the number of characters in the input phrase.
But we know that we discard coefficients and smaller scaling factors, so this
algorithm is really just O(n). These are just a few of the basic data
structures you'll need to be able to work with to develop your own algorithms.
In fact, arrays form the backbone to most other data structures, and are
mandatory to understanding them. 
