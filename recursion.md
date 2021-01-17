# recursion

In some of the last few videos, I’ve shown algorithms that use recursion – that is, they invoke themselves multiple times with new data each time. We’re going to take a moment to cover how recursion actually works, and then we’ll discuss some other concepts you should know for algorithm design. As I’ve mentioned previously, recursion is when an algorithm or function calls itself, where the new execution is working with different data. Even in computer systems with multiple cores or processors, execution tends to be done sequentially. In fact, program execution is handled by a stack. When a new function is invoked, that invocation is pushed to the top of the stack. When the computer begins execution again, that new invocation is peeked, and popped off when it completes. If a function returns a value, it typically ends the execution of that function, but otherwise that occurs when the last line of code in that function finishes running. A function isn’t popped off the stack until execution finishes, and if that function invokes another function – even another copy of itself, that function is pushed on top of the function that called it. Ergo, when you have a chain of function invocations, they are added to the stack and resolved backwards. 

There are few situations where recursion is absolutely required – often times you can implement a recursive algorithm iteratively, but perhaps with a loss of some performance, and arguably some elegance. In truth, once you get used to them, recursive solutions can make more intuitive sense. Typically, you can recognize a recursive problem when you see the phrase, “…to compute the nth…” or “…to compute all…”. Recognizing recursion requires understanding the difference between an algorithm’s instructions and data set. If you are performing the same tasks over and over, but with evenly adjusted data each time, the problem is a candidate for recursion. 

As an example, let’s look at an algorithm that computes the xth number in a Fibonacci sequence. A Fibonacci sequence starts with 0, then 1. After that, each successive number is the sum of the two previous numbers. So the sequence goes 0, 1, 1, 2, 3, 5, 8, etc. Designing an algorithm for this is easy. Since we know what the base case is – 0 and 1, we will start at position x and work backwards. Our recursive algorithm returns 0 or 1 if the position is 0 or 1, but otherwise it computes the Fibonacci number for that position. This recursively invokes the calculation of the sequence value for the previous position, and the position before that. 

```
algorithm fibonacci is
  input: x - the position of the fib num
  output: the fibonacci number at pos. x
  
  if (x == 0)
    return 0
    
  if (x == 1)
    return 1
    
  return fibonacci(x - 1) + fibonacci (x-2)
```

Here’s a diagram of this algorithm in action. We’re going to start at position 3. When we call Fibonacci for the position 3, the algorithm invokes the Fibonacci algorithm for positions 2Next, the invocation for position 2 is called. This invokes the algorithm again for positions 1 and 0and the call for position 1 returns 1 to the same function. The invocation for position 0 returns the value 0 to the call for position 2,Finally the call for position 2 can return the result of 0 + 1 to the call for position 3. and the call for position 1 can return 1 to the same function. Now position 3 can return the value for the equation 1 + 1, which is 2. 

So what’s the runtime of this algorithm? Well, it’s tempting to say O(n^2), since each call invokes two other calls. Or perhaps O(n), because each call only performs an O(1) operation. But to get to the root of the matter, let’s draw out each call as a tree. 

Fibonacci for position 3 invokes 2 and 1. Fibonacci for 2 invokes 0 and 1. We can see that at each level, the number of calls increases exponentially. But there’s always 2 base cases that every call will devolve into. If you grow the list, you’ll see that it actually scales at a rate of O(2^n), which is terrible! If you wanted to compute just the 50th Fibonacci number, it would take just over 1 quadrillion operations. On a modern processor that performs 200 billion operations per second, it would still take over an hour to compute that. 

This brings us to our next topic, memoization. Not memorization, but close. When we think about what the Fibonacci sequence is – just a linear sequence of numbers – then finding the value at position x should only require x previous calculations, right? What our algorithm really needs in order to execute in any reasonable amount of time is a way to memorize the previous values. This is called memoization for what I am sure is a good reason. 

Let’s rewrite our Fibonacci algorithm so that it also accepts an array of numbers, which will store our previously computed values. The value at index 0 will be the number at position 0 of the sequence, and so on. Now our algorithm looks like this. 

```
algorithm fibonacci is
  input: x - the position of the fib num to be calculated
   let memo[] be a new int array of size x+1
   
   return memoFib(x, memo[])
   
algorithm memoFib is
  input: x - the position of the fibonacci number to be calculated
    memo[] - an array of size x+1 that remembers fib nums
  output: the fibonacci numberat position x
  
  if (x == 0)
    return 0
    
  if (x == 1)
    return 1
    
  if (memo[] is empty)
    memo[x] = memoFib(x - 1, memo) + memoFib(x - 2, memo)
    
  return memo[x]

```

We still invoke this algorithm by invoking Fibonacci and passing in x, the position whose value we want to compute. This invokes our actual recursive algorithm named memoFib, and sends both X and a new array of size x + 1. This array is named memo. If the value of X is 0 or 1, we still return our base cases as before. Otherwise, we check the value stored in position x of our memo array. Some languages have empty array indexes default to null, or some value like 0. If that array index is empty, then we fill it by computing the Fibonacci value for previous positions, just like before. 

The catch is that by storing those positional values in our array and checking that array first, we prevent redundant calls. If we draw this execution path as a tree again, we see that memoFib(4) calls memoFib(3) and memoFib(2).  memoFib(3) calls memoFib(2), which calls memoFib(0) and (1), and caches the result. That cache is now used to calculate memoFib(3), which is cached to compute memoFib(4). Now the number of calls is somewhere between n and 2n, which just gives us O(n) performance. This actually saves memory too – remember that with a recursive algorithm, each function call cannot finish until all of its own calls finish executing. This means those functions are sitting in memory until execution reaches them again, which can take a while. With large computations, you might run out of memory before your execution ever starts to work its way back down the stack. 

Recursion is a powerful tool for designing elegant algorithms, but you can quickly run into performance issues as they scale exponentially. You can improve that performance again with memoization, by eliminating redundant recursions. 
