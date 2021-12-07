This page explains some terms that you will encounter in the RE2 codebase.

**BitState:** The execution engine that implements backtracking search AKA depth-first search. Uses a stack structure to eschew recursion and a bitmap structure to guarantee linear-time performance. Used only when the pattern and the input string are small.

**bytecode:** The array of instructions (i.e. opcodes and operands) that defines an automaton.

**bytemap:** The array that maps all 256 byte values to equivalence classes, which are sets of byte values that the bytecode treats indistinguishably. For example, the bytecode for `\d+` has two equivalence classes: the byte values from `'0'` to `'9'`; and all other byte values. Used by the DFA and OnePass execution engines.

**DFA:** The execution engine that implements Deterministic Finite Automaton search. Fundamentally similar to the NFA execution engine, but caches the results of computations in exchange for ignoring submatches. Supports concurrent lookups and serialised inserts per `DFA` object. Used as the workhorse.

**execution engine:** An implementation of bytecode execution in a particular style.

**NFA:** The execution engine that implements Nondeterministic Finite Automaton search AKA breadth-first search. Computes all possible results for each input byte. Used only as the last resort.

**OnePass:** The execution engine that implements one-pass search. Uses its own bytecode, which is a precomputed DFA. Used only when the pattern is unambiguous and the search is anchored at the start and no more than four submatches are requested.

**pattern:** A regular expression in textual form. Parsed into a `Regexp`.

**`Prog`:** A regular expression in compiled form. Contains the bytecode, the bytemap, the OnePass bytecode (if applicable), two `DFA` objects (lazily allocated) et cetera.

**`Regexp`:** A regular expression in parsed form. An acyclic graph of reference-counted nodes, so intra- and inter-graph sharing of nodes is possible. Compiled into a `Prog`.

**`Rune`:** A character in the sense of character encoding, not in the sense of `char`. More properly known as a code point, but RE2 uses libutf from Plan 9.
