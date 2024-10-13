## Challenges

1. Pick an open source implementation of a language you like. Download the
   source code and poke around in it. Try to find the code that implements the
   scanner and parser. Are they handwritten, or generated using tools like Lex
   and Yacc? (.l or .y files usually imply the latter.)

    - I have chosen typescript as one such language, it's
      [scanner](https://github.com/microsoft/TypeScript/blob/main/src/compiler/scanner.ts)
      and
      [parser](https://github.com/microsoft/TypeScript/blob/main/src/compiler/parser.ts)
      are handwritten and can be found at links attached, both of these
      components are implemented without the use of tools like Yacc or Lex.

2. Just-in-time compilation tends to be the fastest way to implement
   dynamically typed languages, but not all of them use it. What reasons are
   there to not JIT?

   - High Memory and Resource Overhead due to both the runtime optimizations
     and execution on the same time.
   - JIT leads to slower startup times which is noticeable for the first run.
   - For short lived programs or where the code paths aren't repeatedly
     frequently, JIT won't outweigh the overhead costs.
   - A JIT compiler needs to produce machine code for the specific architecture
     on which it runs, which can make portability across different platforms
     more difficult.

3. Most Lisp implementations that compile to C also contain an interpreter that
   lets them execute Lisp code on the fly as well. Why?

   - Lisp is known for its interactive development model, where developers
     frequently write and test code in small increments. Having an interpreter
     allows developers to evaluate expressions interactively without needing to
     recompile the entire program. This helps in rapidly prototyping and
     testing code​
