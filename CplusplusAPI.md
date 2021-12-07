# Syntax

In POSIX mode, RE2 accepts standard POSIX (egrep) syntax regular expressions.
In Perl mode, RE2 accepts most Perl operators.  The only excluded ones are
those that require backtracking (and its potential for exponential runtime)
to implement.  These include backreferences (submatching is still okay)
and generalized assertions.  The [[Syntax]] page documents the supported Perl-mode syntax in detail.  The default is Perl mode.

# Matching Interface

There are two basic operators: ` RE2::FullMatch ` requires the regexp to match the entire input text, and ` RE2::PartialMatch ` looks for a match for a substring of the input text, returning the leftmost-longest match in POSIX mode and the
same match that Perl would have chosen in Perl mode.

Examples:
```cpp
assert(RE2::FullMatch("hello", "h.*o"))
assert(!RE2::FullMatch("hello", "e"))

assert(RE2::PartialMatch("hello", "h.*o"))
assert(RE2::PartialMatch("hello", "e"))
```

# Submatch Extraction

Both matching functions take additional arguments in which submatches will be stored.  The argument can be a ` string `, or an integer type, or the type ` StringPiece `.
A ` StringPiece ` is a pointer to the original input text, along with a count.  It behaves like a string but doesn't carry its own storage.  Like when using a pointer, when using a ` StringPiece ` you must be careful not to use it once the original text has been deleted or gone out of scope.

Examples:
```cpp
// Successful parsing.
int i;
string s;
assert(RE2::FullMatch("ruby:1234", "(\\w+):(\\d+)", &s, &i));
assert(s == "ruby");
assert(i == 1234);

// Fails: "ruby" cannot be parsed as an integer.
assert(!RE2::FullMatch("ruby", "(.+)", &i));

// Success; does not extract the number.
assert(RE2::FullMatch("ruby:1234", "(\\w+):(\\d+)", &s));

// Success; skips NULL argument.
assert(RE2::FullMatch("ruby:1234", "(\\w+):(\\d+)", (void*)NULL, &i));

// Fails: integer overflow keeps value from being stored in i.
assert(!RE2::FullMatch("ruby:123456789123", "(\\w+):(\\d+)", &s, &i));
```

# Pre-Compiled Regular Expressions

The examples above all recompile the regular expression on each call.
Instead, you can compile it once to an RE2 object and reuse that object for each call.

Example:
```cpp
RE2 re("(\\w+):(\\d+)");
assert(re.ok());  // compiled; if not, see re.error();

assert(RE2::FullMatch("ruby:1234", re, &s, &i));
assert(RE2::FullMatch("ruby:1234", re, &s));
assert(RE2::FullMatch("ruby:1234", re, (void*)NULL, &i));
assert(!RE2::FullMatch("ruby:123456789123", re, &s, &i));
```

# Options

The constructor takes an optional second argument that can
be used to change RE2's default options.
For example, the predefined ` Quiet ` options silence error
message printing when a regular expression fails to parse:

```cpp
RE2 re("(ab", RE2::Quiet);  // don't write to stderr for parser failure
assert(!re.ok());  // can check re.error() for details
```

Other useful predefined options are ` Latin1 ` (disable UTF-8) and ` POSIX ` (use POSIX syntax and leftmost longest matching).

You can also declare your own RE2::Options object and then configure it as you like.
See the [header](https://github.com/google/re2/blob/master/re2/re2.h) for the full set of options.

# Unicode Normalization

RE2 operates on Unicode code points: it makes no attempt at normalization. For example, the regular expression /ü/ (U+00FC, u with diaeresis) does not match the input "ü" (U+0075 U+0308, u followed by combining diaeresis). Normalization is a long, involved topic. The simplest solution, if you need such matches, is to normalize both the regular expressions and the input in a preprocessing step before using RE2. For more details on the general topic, see http://www.unicode.org/reports/tr15/.

# Additional Tips and Tricks

For advanced usage, like constructing your own argument lists,
or using RE2 as a lexer, or parsing hex, octal, and C-radix numbers,
see [re2.h](https://github.com/google/re2/blob/master/re2/re2.h).
