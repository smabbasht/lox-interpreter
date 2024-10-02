## Chapter 2 - A Map of the Territory

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
  instructions for some real chip. Wirth caled p-code (portable) which we now
  say `bytecode` since each instruction is usually just a byte long.

### Virtual Machine
- A compiler that produces output must also translate it to machine code since
  there is no real chip that speaks bytecode, you still have to do work for
  each chip you support.
- A `virtual machine` could help us here, a VM is a program that emulates a
  hypothetical chip supporting your virtual architecture at runtime. Running
  bytecode in a VM is slower than translating it to native code ahead of time
  because every instruction must be simulated at runtime each time it executes
  but you get simplicity and portability in return.
    



1. If we choose real machine code than 
