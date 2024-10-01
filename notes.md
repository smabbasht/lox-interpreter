## Chapter 2 - A Map of the Territory

### Scanning
- The first step is scanning, also known as lexing, or  lexical analysis.
- A scanner (or lexer) takes in the linear stream of characters and chunks them
  together into a series of something more akin to “words”. In programming
  languages, each of these words is called a token. Some tokens are single
  characters, like ( and ,. Others may be several characters long, like numbers
  (123), string literals ("hi!"), and identifiers (min).
- Some characters in a source file don’t actually mean anything. Whitespace is
  often insignificant, and comments, by definition, are ignored by the
  language. The scanner usually discards these, leaving a clean sequence of
  meaningful tokens.
### Parser
- A parser takes the flat sequence of tokens and builds a tree structure that
  mirrors the nested nature of the grammar.
- we humans still manage to use those simple grammars incorrectly, so the
  parser’s job also includes letting us know when we do by reporting syntax
  errors.
### Static Analysis
- The first bit of analysis that most languages do is called binding or
  resolution. For each identifier, we find out where that name is defined and
  wire the two together. This is where scope comes into play—the region of
  source code where a certain name can be used to refer to a certain
  declaration.
- If the language is statically typed, this is when we type check. Once we know
  where a and b are declared, we can also figure out their types. Then if those
  types don’t support being added to each other, we report a type error.
- All this semantic insight that is visible to us from analysis needs to be
  stored somewhere. There are a few ways to do that:
  - Store as an attribute on syntax tree itself.
  - Store in a lookup table with keys as symbol called symbol table.
  - Transform tree into a new DS that expresses the semantic of the code.
### Intermediate representation
- 
