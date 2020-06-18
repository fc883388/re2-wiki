# Black Lives Matter. [Support the Equal Justice Initiative.](https://support.eji.org/give/153413/#!/donation/checkout)

_**Safety is RE2's raison d'être.**_

RE2 was designed and implemented with an explicit goal of being able to handle regular expressions from untrusted users without risk. One of its primary guarantees is that the match time is linear in the length of the input string. It was also written with production concerns in mind: the parser, the compiler and the execution engines limit their memory usage by working within a configurable budget – failing gracefully when exhausted – and they avoid stack overflow by eschewing recursion.

It is not a goal to be faster than all other engines under all circumstances. Although RE2 guarantees linear-time performance, the linear-time constant varies depending on the overhead entailed by safe handling of the regular expression. In a sense, RE2 behaves pessimistically whereas backtracking engines behave optimistically, so it can be outperformed in various situations.

It is also not a goal to implement all of the features offered by Perl, PCRE and other engines. As a matter of principle, RE2 does not support constructs for which only backtracking solutions are known to exist. Thus, backreferences and look-around assertions are not supported.

For more information, please refer to Russ Cox's articles on regular expression theory and praxis:

* [Regular Expression Matching Can Be Simple And Fast](https://swtch.com/~rsc/regexp/regexp1.html)
* [Regular Expression Matching: the Virtual Machine Approach](https://swtch.com/~rsc/regexp/regexp2.html)
* [Regular Expression Matching in the Wild](https://swtch.com/~rsc/regexp/regexp3.html)
