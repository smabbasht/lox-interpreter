# Chapter 2 - A Map of the Territory

## The parts of a language

### Scanning
- The first step is `scanning`, also known as `lexing`, or  `lexical analysis`.
- A `scanner` (or lexer) takes in the linear stream of characters and chunks them
  together into a series of something more akin to “words”. In programming
  languages, each of these words is called a token. Some tokens are single
  characters, like ( and ,. Others may be several characters long, like numbers
  (123), string literals ("hi!"), and identifiers (min).
- Some characters in a source file don’t actually mean anything. Whitespace is
  often insignificant, and comments, by definition, are ignored by the
  language. The scanner usually discards these, leaving a clean sequence of
  meaningful tokens.
### Parser
- A `parser` takes the flat sequence of tokens and builds a tree structure that
  mirrors the nested nature of the grammar.
- we humans still manage to use those simple grammars incorrectly, so the
  parser’s job also includes letting us know when we do by reporting syntax
  errors.
### Static Analysis
- `Binding` or `resolution` is the first bit of analysis that most languages do
  i-e for each identifier, we find out where that name is defined and wire the
  two together. 
- This is where we `type-check` if the language is statically typed, For e.g in
  a+b we know through parsing that a and b are being added, here we know
  through binding, their declarations so we know their types, so we can check
  that whether addition is defined for their types.
- Scopes are also defined here that is a region of code where certain name is
  associated with certain declaration.
- All this semantic insight that is visible to us from analysis needs to be
  stored somewhere. There are a few ways to do that:
  - Store as an attribute on syntax tree itself.
  - Store in a lookup table with keys as symbol called symbol table.
  - Transform tree into a new DS that expresses the semantic of the code.

> Everything until this point is called front-end of the implementation which is
> specific to the language the code is written in, Now comes the middle-end.

### Intermediate representation
- In the middle of front-end and back-end, the code is stored in some
  `Intermediate representation`. This acts as an interface to source and
  destination forms and isn't tightly bound to any of them.
- This front, middle and back-end lets us support multiple source languages
  (Pascal, C, Fortran) and target platforms (like x86_64, ARM).

### Optimization
- Once we understand what user's code means, we can replace the user's code
  with some more performant, logically equivalent code. This is called
  `optimization`.
- `Constant folding` is a simple example, for e.g `let a = 5000/5` can be changed
  with `let a = 1000` at compile time so that we don't need to perform the
  computation at runtime.

> Finally we are in the back-end.

### Code Generation
- The last step is converting it to a form the machine can actually run. In
  other words, `generating code` (or code gen), where “code” here usually refers
  to the kind of primitive assembly-like instructions a CPU runs.
> We now have a decision to make. Do we generate code for a virtual CPU or a
> real one?
- If we generate it real machine code, we get an executable that OS can
  directly load on a chip. Native code is lightning fast but generating it is a
  lot of work. It also means that compiler is tied with a specific
  architecture.
- To get around this, Wirth and Richards from BCPL & Pascal made their
  compilers produce (hypothetical, idealized) virtual machine code instead of
  instructions for some real chip. Wirth called it p-code (portable) which we
  now say `bytecode` since each instruction is usually just a byte long.

### Virtual Machine
- A compiler that produces output must also translate it to machine code since
  there is no real chip that speaks bytecode, you still have to do work for
  each chip you support.
- A `virtual machine` could help us here, a VM is a program that emulates a
  hypothetical chip supporting your virtual architecture at runtime. Running
  bytecode in a VM is slower than translating it to native code ahead of time
  because every instruction must be simulated at runtime each time it executes
  but you get simplicity and portability in return.

### Runtime
- We now have a form of user's program that we can execute. The last step is
  running it. If we compiled it to machine code, we simply tell the operating
  system to load the executable and off it goes. If we compiled it to bytecode,
  we need to start up the VM and load the program into that.
- In both cases, for all but the basest of low level language, we usually need
  some services like garbage collection that our language provides.
- All of this stuff goes at `runtime` so it is appropriately named that.
- In a fully compiled language like `rust` or `go`, the code implementing
  runtime gets inserted into resulting executable whereas languages running
  inside an interpreter have their runtime in VM.

## Shortcuts & Alternate Routes
This was the long route, there are other routes too, for e.gets

### Single-pass compiler
- Single pass compilers interleave parsing, analysis and code generation so
  that output code can be produced in the parser directly, this also means that
  the language doesn't have to allocate an IR, and syntax trees.
- But this restrict the design of the language, you have no intermediate data
  structures to store global info about the program and you don't revisit any
  part so you must have every bit of information needed to compile before
  receiving any expression.
- C and Pascal were designed with this limitation, hence you can't call a
  function in C before defining that because in the early days memory was so
  precious and sometimes the whole source file couldn't be loaded in memory at
  once.

### Tree-walk Interpreters
- Some interpreters begin executing the program right after parsing it to an
  AST, To run the program, they traverse the syntax tree, one branch and a leaf
  at a time evaluating each node as it goes.
- This implementation tends to be slow.

### Transpilers
- If you write a front-end of your language and in the back-end, instead of
  writing the complete back-end yourself, you convert your source code into
  some string that is a valid source code of some other language, This way you
  escape the route off mountain, getting something you can execute. This is
  called source-to-source compiler, trans-compiler or transpiler.
- If the new language is just a skin over the target language then just the
  scanner and parser would suffice the front-end of the new language but if the
  two are semantically different then analysis and even optimization could be
  involved.

### Just-in-time Compilation
- This last one is less of a shortcut and more of an option reserved for
  experts. As we know that the fastest running executable is one that is in
  machine code right? So on the end user's machine when the program is loaded,
  you compile it to native code for the architecture their computer supports.
  Naturally enough, this is called Just-in-time compilation or JIT (rhymes with
  fit).
- HotSpot JVM, Microsoft's Common Language Runtime (CLR), and most JS
  interpreters do this. 
- The most sophisticated JITs insert profiling hooks into generated code to see
  which regions are most performance critical and what kind of data is flowing
  through them , then over time, they'll automatically recompile those hot
  spots with more advanced optimizations.

## Compilers and Interpreters

### What is the difference?
- Compiling is an implementation technique that involves translating a source
  language to some other—usually lower-level—form. When you generate bytecode
  or machine code, you are compiling. When you transpile to another high-level
  language, you are compiling too.
- When we say a language implementation “is a compiler”, we mean it translates
  source code to some other form but does not execute it. The user has to take
  the resulting output and run it themselves.
- Conversely, when we say an implementation “is an interpreter”, we mean it
  takes in source code and executes it immediately. It runs programs “from
  source”.
