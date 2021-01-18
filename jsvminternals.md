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

## call stack

records the current state of execution. having a single thread, js has a single call stack

## event loop

## callback queue

## heap

## webAPIs

