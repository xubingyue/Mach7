Mach7: A PATTERN MATCHING LIBRARY FOR C++
=========================================

by Yuriy Solodkyy <yuriy.solodkyy@gmail.com>


License Agreement (BSD)
-----------------------

*Mach7: Pattern Matching Library for C++*

Copyright 2011-2013, Texas A&M University.
Copyright 2014 Yuriy Solodkyy.
All rights reserved.

Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions are met:

    * Redistributions of source code must retain the above copyright
      notice, this list of conditions and the following disclaimer.

    * Redistributions in binary form must reproduce the above copyright
      notice, this list of conditions and the following disclaimer in the
      documentation and/or other materials provided with the distribution.

    * Neither the names of Mach7 project nor the names of its contributors
      may be used to endorse or promote products derived from this software
      without specific prior written permission.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND
ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED
WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED.
IN NO EVENT SHALL THE COPYRIGHT HOLDERS OR CONTRIBUTORS BE LIABLE FOR ANY
DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES
(INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES;
LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND
ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
(INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS
SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.

Mach7 by Example
----------------

// Fibonacci numbers
int fib(int n) 
{ 
    var⟨int⟩ m; 
    Match(n) {
    Case(1)     return 1;
    Case(2)     return 1;
    Case(2*m)   return sqr(fib(m+1)) − sqr(fib(m−1));
    Case(2*m+1) return sqr(fib(m+1)) + sqr(fib(m));
    } EndMatch
}

// Lambda calculator
struct Term       { virtual ∼Term() {}     };
struct Var : Term { std:: string name;     };
struct Abs : Term { Var& var; Term& body;  };
struct App : Term { Term& func; Term& arg; };

Term∗ eval(Term* t) {
    var⟨const Var&⟩ v; var⟨const Term&⟩ b,a;
    Match(*t) {
    Case(C⟨Var⟩())              return &match0;
    Case(C⟨Abs⟩())              return &match0;
    Case(C⟨App⟩(C⟨Abs⟩(v,b),a)) return eval(subs(b,v,a)); 
    Otherwise() std:: cerr ≪ ”error”; return nullptr ;
} EndMatch

Building sources
----------------

Using GCC (4.4 or later) or Clang (5.1 or later)
 * make
    - builds .exe files from all the .cpp files in current directory.
 * make timings
    - builds all combinations of encodings, syntax and benchmarks out of 
      skeleton.cxx for timing purposes
 * make syntax
    - builds all combinations of configuration flags supported by the library to 
      make sure nothing was omitted
 * make test
    - runs all the .exe files in the current folder

Using Visual C++ (2010 or later)
 * test-pm-timing.bat
    - builds all combinations of encodings, syntax and benchmarks out of 
      skeleton.cxx for timing purposes (same as "make timings" for Visual C++)
 * test-pgo.bat
    - compiles and performs profile-guided optimizations on all files passed as 
      arguments
 * test-pm.bat
    - builds sources varying amount of derived classes and virtual functions in 
      them
 * test-pm-daily.bat
    - builds all files in the test suite
 * test-pm-daily-pgo.bat
    - builds all files in the test suite and performs profile-guided 
      optimizations on them
 * ttt.bat
    - converts the summary of outputs into a latex definitions used in the 
      performance table

Known bugs and limitations
--------------------------

The following files crash GCC 4.4.5 on my Fedora 13 box. If they do on yours 
too, just delete them, they are all test cases anyways.
 - extractor.cpp
 - shape2.cpp
 - shape4.cpp
 - shape5.cpp
 - shape6.cpp7
 - shape.cpp
 - numbers.cpp
 - category.cpp
 - exp.cpp

Publications
------------

 * Y.Solodkyy, G.Dos Reis, B.Stroustrup. "[Open Pattern Matching for C++: Extended Abstract](https://parasol.tamu.edu/~yuriys/papers/OPM13EA.pdf)" In Proceedings of the 2013 companion publication for conference on Systems, programming, & applications: software for humanity (SPLASH '13). ACM, New York, NY, USA, pp. 97-98. [pdf](https://parasol.tamu.edu/~yuriys/papers/OPM13EA.pdf), [slides](https://parasol.tamu.edu/~yuriys/presentations/2013-10-27-GPCE-PatternMatching.pptx), [notes](https://parasol.tamu.edu/~yuriys/presentations/2013-10-27-GPCE-PatternMatching-Notes.pdf), [poster](https://parasol.tamu.edu/~yuriys/posters/Mach7.pdf), [project](http://parasol.tamu.edu/mach7/)
 * Y.Solodkyy, G.Dos Reis, B.Stroustrup. "[Open Pattern Matching for C++](https://parasol.tamu.edu/~yuriys/papers/OPM13.pdf)" In Proceedings of the 12th international conference on Generative programming: concepts & experiences (GPCE '13). ACM, New York, NY, USA, pp. 33-42. [pdf](https://parasol.tamu.edu/~yuriys/papers/OPM13.pdf), [slides](https://parasol.tamu.edu/~yuriys/presentations/2013-10-27-GPCE-PatternMatching.pptx), [notes](https://parasol.tamu.edu/~yuriys/presentations/2013-10-27-GPCE-PatternMatching-Notes.pdf), [poster](https://parasol.tamu.edu/~yuriys/posters/Mach7.pdf), [project](http://parasol.tamu.edu/mach7/)
 * Y.Solodkyy. "[Simplifying the Analysis of C++ Programs](https://parasol.tamu.edu/~yuriys/papers/SOLODKYY-DISSERTATION-2013.pdf)" Ph.D. Thesis. Texas A&M University. August 2013. [slides](https://parasol.tamu.edu/~yuriys/presentations/2013-05-22-PhdDefense.pptx)
 * Y.Solodkyy, G.Dos Reis, B.Stroustrup. "[Open and Efficient Type Switch for C++](https://parasol.tamu.edu/~yuriys/papers/TS12.pdf)" In Proceedings of the ACM international conference on Object Oriented Programming Systems Languages and Applications (OOPSLA '12). ACM, New York, NY, USA, pp. 963-982. [pdf](https://parasol.tamu.edu/~yuriys/papers/TS12.pdf), [slides](https://parasol.tamu.edu/~yuriys/presentations/2012-10-25-OOPSLA-TypeSwitch.pptx), [notes](https://parasol.tamu.edu/~yuriys/presentations/2012-10-25-OOPSLA-TypeSwitch-Notes.pdf), [poster](https://parasol.tamu.edu/~yuriys/posters/Mach7.pdf), [extras](https://parasol.tamu.edu/~yuriys/pm/), [project](http://parasol.tamu.edu/mach7/)]

Support
-------

Please contact Yuriy Solodkyy at yuriy.solodkyy@gmail.com with any questions regarding Mach7.