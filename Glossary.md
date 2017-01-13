This page explains some terms that you will encounter in the RE2 codebase.

**BitState:**

**bytecode:** An array of instructions (i.e. opcodes and operands) that defines an automaton.

**bytemap:** An array that maps all 256 byte values to equivalence classes, which are sets of byte values that the corresponding bytecode treats indistinguishably. For example, the bytecode for `\d+` has two equivalence classes: the byte values from `'0'` to `'9'`; and all other byte values. Used by the DFA and OnePass execution engines.

**DFA:**

**execution engine:** An implementation of bytecode execution in a particular style.

**NFA:**

**OnePass:**

**pattern:** A regular expression in textual form. Parsed into a `Regexp`.

**`Prog`:** A regular expression in compiled form. Contains the bytecode, the bytemap, the OnePass bytecode (if applicable), two DFAs (lazily allocated) et cetera.

**`Regexp`:** A regular expression in parsed form. An acyclic graph of reference-counted nodes, so intra- and inter-graph sharing of nodes is possible. Compiled into a `Prog`.

**`Rune`:** A character in the sense of character encoding, not in the sense of `char`. More properly known as a code point, but RE2 uses libutf from Plan 9.
