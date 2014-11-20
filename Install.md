<b>Quick links:</b> <a href='http://code.google.com/p/re2/source/browse'>browse</a> | <a href='http://code.google.com/p/re2/source/list'>changes</a>

RE2 should install on any modern Unix clone with g++.

<pre>
hg clone https://re2.googlecode.com/hg re2<br>
cd re2<br>
make test<br>
make install<br>
make testinstall</pre>
(On BSD systems, use ` gmake ` instead of ` make `.)

No attempt has been made to make RE2 compile on Windows, but if anyone would like to try, patches would be welcomed.

For documentation on how to use RE2, see the comment at the top of <a href='http://code.google.com/p/re2/source/browse/re2/re2.h'>re2/re2.h</a>.

[How to contribute code.](wiki/Contribute)

Mail [re2-dev](http://groups.google.com/group/re2-dev) with problems.

RE2's native language is C++.<br />
An Inferno wrapper is at http://code.google.com/p/inferno-re2/.<br />
A Python wrapper is at http://github.com/facebook/pyre2/.<br />
A Ruby wrapper is at http://github.com/axic/rre2/.<br />
An Erlang wrapper is at http://github.com/tuncer/re2/.<br />
A Perl wrapper is at http://search.cpan.org/~dgl/re-engine-RE2-0.05/lib/re/engine/RE2.pm.<br />
An Eiffel wrapper is at http://sourceforge.net/projects/eiffelre2/<br />