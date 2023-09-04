<b>Quick links:</b> <a href='https://github.com/google/re2'>browse</a> | <a href='https://github.com/google/re2/commits/master'>changes</a>

RE2 should build and run on any modern Unix clone with GCC or Clang.

<pre>
git clone https://code.googlesource.com/re2
cd re2
make
make test
make install
make testinstall
</pre>
(On BSD systems, use `gmake` instead of `make`.)

Building RE2 requires Abseil (https://github.com/abseil/abseil-cpp) to be installed on your system. Building the testing for RE2 requires GoogleTest (https://github.com/google/googletest) and Benchmark (https://github.com/google/benchmark) to be installed as well.

Bazel and CMake are also supported. The latter enables generation of Visual Studio and Xcode projects as well as Cygwin, MinGW and MSYS makefiles. Bug reports and/or fixes are welcome!

Your compiler must support C++14.<br>
_Visual Studio users: You need Visual Studio 2019 or later._<br>
_Cygwin users: You must run CMake from the Cygwin command line, not the Windows command line._<br>

CMake has two ways to use a dependency: `add_subdirectory()`, which is when the dependency's **_sources_** are in a subdirectory of your project; and `find_package()`, which is when the dependency's **_binaries_** have been built and installed somewhere on your system. The Abseil documentation walks through the former [here](https://abseil.io/docs/cpp/quickstart-cmake) versus the latter [here](https://abseil.io/docs/cpp/tools/cmake-installs). Once you get Abseil working, getting RE2 working will be a very similar process and, either way, `target_link_libraries(… re2::re2)` should Just Work™.

For documentation on how to use RE2, see the comment at the top of <a href='https://github.com/google/re2/blob/master/re2/re2.h'>re2/re2.h</a>.

[How to contribute code.](Contribute)

Mail [re2-dev](https://groups.google.com/group/re2-dev) with problems.

RE2's native language is C++.<br>
<br>
The Python wrapper is at https://github.com/google/re2/tree/abseil/python<br>
and on PyPI (https://pypi.org/project/google-re2/).<br>
<br>
A C wrapper is at https://github.com/marcomaggi/cre2/.<br>
A D wrapper is at https://github.com/ShigekiKarita/re2d/ and on DUB (code.dlang.org).<br>
An Erlang wrapper is at https://github.com/dukesoferl/re2/ and on Hex (hex.pm).<br>
An Inferno wrapper is at https://github.com/powerman/inferno-re2/.<br>
A Node.js wrapper is at https://github.com/uhop/node-re2/ and on NPM (npmjs.com).<br>
An OCaml wrapper is at https://github.com/janestreet/re2/ and on OPAM (opam.ocaml.org).<br>
A Perl wrapper is at https://github.com/dgl/re-engine-RE2/ and on CPAN (cpan.org).<br>
An R wrapper is at https://github.com/girishji/re2/ and on CRAN (cran.r-project.org).<br>
A Ruby wrapper is at https://github.com/mudge/re2/ and on RubyGems (rubygems.org).<br>
A WebAssembly wrapper is at https://github.com/google/re2-wasm/ and on NPM (npmjs.com).<br>
