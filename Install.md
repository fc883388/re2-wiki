<b>Quick links:</b> <a href='https://github.com/google/re2'>browse</a> | <a href='https://github.com/google/re2/commits/master'>changes</a>

RE2 should build and run on any modern Unix clone with GCC or Clang.

<pre>
git clone https://code.googlesource.com/re2<br>
cd re2<br>
make test<br>
make install<br>
make testinstall</pre>
(On BSD systems, use `gmake` instead of `make`.)

Bazel and CMake are also supported. The latter enables generation of Visual Studio and Xcode projects as well as Cygwin, MinGW and MSYS makefiles. Bug reports and/or fixes are welcome!

Your compiler must support C++11. In particular, the DFA execution engine depends on C++11 atomics.<br>
_Visual Studio users: You need Visual Studio 2013 or later. Building a DLL is not currently supported._<br>
_Cygwin users: You must run CMake from the Cygwin command line, not the Windows command line._<br>

For documentation on how to use RE2, see the comment at the top of <a href='https://github.com/google/re2/blob/master/re2/re2.h'>re2/re2.h</a>.

[How to contribute code.](Contribute)

Mail [re2-dev](https://groups.google.com/group/re2-dev) with problems.

RE2's native language is C++.<br>
<br>
A C wrapper is at https://github.com/marcomaggi/cre2/.<br>
An Erlang wrapper is at https://github.com/tuncer/re2/.<br>
An Inferno wrapper is at https://github.com/powerman/inferno-re2/.<br>
A Node.js wrapper is at https://github.com/uhop/node-re2/ and on NPM.<br>
An OCaml wrapper is at https://github.com/janestreet/re2/ and on OPAM.<br>
A Perl wrapper is at https://github.com/dgl/re-engine-RE2/ and on CPAN.<br>
A Python wrapper is at https://github.com/facebook/pyre2/.<br>
An R wrapper is at https://github.com/qinwf/re2r/.<br>
A Ruby wrapper is at https://github.com/mudge/re2/.<br>