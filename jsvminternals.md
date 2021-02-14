# JS VM internals Notes

## General Overivew

1. JS source code is parsed with the *parser* to create the *Abstract Syntax Tree*
2. the AST is processed by the *interpreter* to produce *bytecode*
3. bytecode is run by the JS VM.
4. while bytecode is running in the *interpreter*, an *optimizing compiler* is run parallel, receiving *profiling data* from the running bytecode and receiving bytecode from the interpreter.
5. optimized bytecode is produced. bytecode can be deoptimized if needed be sending it back through the interpreter.

## major engines

- v8 (google's chromium)
- spidermonkey (mozilla's firefox)
- chakra (microsoft's chromium)
- jsc (original webkit; safari and react native)
 
## v8 runtime

## thread of execution

### Feature 1 of JS

starting in the *global execution context*, js goes through code line by line and executes each line. that's the "thread of execution".

### Feature 2

identifiers are things like variables (data) and functions (code), which reference things stored in memory.

On a function call, the thread finds the referenced area of memory and runs the code found there *in a new execution context*. Local memory is the area where new function call's code is stored, hench why it's only available to the current execution context. On return, the thread of execution is asked to go look for the return value in local memory to hand to the calling context. Of course, js is single threaded, so changing execution contexts on a function call means that the calling execution context is stopped.

### Feature 3

js keeps track of what execution context is currently running in the call stack. whatever's on the top of the stack is the current execution context. `return` can be seen as the keyword that indicates that js has to go back to the calling context. When everything's been popped off, the execution context is global().

not to be confused with block scope; things like ifs and loops get their own protected namespace within the execution context. 

## call stack

records the current state of execution. having a single thread, js has a single call stack

## event loop

## callback queue

## heap

## webAPIs

