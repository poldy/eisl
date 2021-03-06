# Policy 

I want to keep Easy-ISLisp as small and simple as possible.

I was a fan of Scheme. It was around R3RS ~ R5RS. I fell in love with Scheme's simple and elegant design philosophy. 
However, after R6RS, Scheme changed its policy to become huge.
I hated the recent huge Scheme.

Around that time, I learned about the ISLisp standard. It is very simple and compact. I fell in love with this.
For this reason I want to keep Easy-IS Lisp as small and simple as possible.

## Hints for C Coding

Although we all love to write Lisp, a lot of the interpreter had to be written in C.

This section contains some hints on how to write more robust C code.
A main aim is to be welcoming to new contributors of different abilities.
In corporate life there would be a mandatory "coding standard", but I'd really like to avoid stuff like that, not least in order to accept help from a wide range of volunteers.
It's ok to assume intermediate knowledge of C (e.g. understanding pointers), but there should be no need to know all the nooks and crannies of the ISO standard.
So fancy tricks are to be avoided, and tools should be used where possible to help.

Although there's no need to follow it, the
[OpenBSD style guide](https://man.openbsd.org/style)
is recommended as some nice background reading.

First, try to write idiomatic C.
C17 is ok, because we're assuming the compiler is a recent release of gcc or clang anyway.
C++ (specifically the
["Embedded" subset](https://en.wikipedia.org/wiki/Embedded_C%2B%2B))
[was considered](https://github.com/sasagawa888/eisl/issues/95),
but in the end it was decided to not use it.

Here are some miscellaneous recommendations, I'm sure I've missed lots:
* Favour structured programming instead of gotos
* Don't Repeat Yourself
* Let the typechecker help you, e.g. use enums & proper bool types
* Part of this is to try avoid the preprocessor, e.g. by using `static inline` for macros, `static const int x = 42;` instead of `#define`
* Avoid numeric literals in the body of code for things like array sizes ("magic" numbers), define them as constants once

You can get a lot done in just ISO C, but use of standard UNIX libraries is ok, e.g. defined by standards like
[UNIX V7](https://en.wikipedia.org/wiki/Single_UNIX_Specification),
X/Open and IETF RFCs.
Please don't write Linux-specific code.

If at some point it seems that a C++ feature would be really useful, it may actually be available as a C library.
An interesting library is
[cii](https://github.com/drh/cii),
but we probably don't want to use it quite yet.
Even though we decided not to use C++, writing
[Object-Oriented C](https://www.cs.rit.edu/~ats/)
looks potentially interesting but would have to be evaluated properly.
It's best to think of everything in this paragraph as a research project that may not or may not be ready for production.

As regards tools, the compiler warnings are all switched on.
And there is a rule to run cppcheck in the top-level makefile.
There is no need to have zero warnings, but at least the reason for them should be understood.
We could use an indent tool at some time in the future (e.g.
[GNU Indent](https://www.gnu.org/software/indent/) or
[Artistic Style](http://astyle.sourceforge.net/)),
but for now just try to fit in with the existing code (this applies to naming conventions too).

The source code is formatted with GNU indent. Barkley style with -orig option. 
