This page explains some terms that you will encounter in the RE2 codebase.

**BitState:**

**bytecode:**

**bytemap:**

**DFA:**

**execution engine:**

**`Inst`:**

**NFA:**

**OnePass:**

**pattern:** A regular expression in textual form. Parsed into a `Regexp`.

**`Prog`:** A regular expression in compiled form. Contains the bytecode, the bytemap, the OnePass bytecode (if applicable), two DFAs (lazily allocated) et cetera.

**`Regexp`:** A regular expression in parsed form. An acyclic graph of reference-counted nodes, so intra- and inter-graph sharing of nodes is possible. Compiled into a `Prog`.

**`Rune`:** A character in the sense of character encoding, not in the sense of `char`. More properly known as a code point, but RE2 uses libutf from Plan 9.
