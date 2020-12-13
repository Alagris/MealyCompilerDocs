Dokument wizji projektu

Nazwa projektu: Solomonoff

Autorzy: Aleksander Mendoza, Bogdan Bondar, Marcin Jabłoński

Data: 13.12.2020

1. Executive summary (max. 150 słów)

This project focuses on research in the field of automata theory and inductive inference. While many existing libraries already provide support for general purpose automata and implement various related algorithms, this project takes a slightly different approach. The primary tool for working with the library, is through doman specific language of regular expressions. Most of the things can be done without writing even a single line of Java code. 

The main applications concern formal methods, natural language processing, state-based system modeling, pattern recognition, inductive inference and machine learning. It can be of great help for researchers as well as can be used on industrial scale.

The greatest competitor for Solomonoff is Google's OpenFST project. Solomonoff introduces dozens of improvements. The most important being efficiency improvements, symbolic ranges, nondeterminism detection and type system.

2. Cel i grupa docelowa (min. 150 słów)

The goal is provide an better alternative for OpenFST. Solomonoff strives to provide improvement in the following domains:

- OpenFst has Matcher that was meant to compactify ranges. In Solomonoff all transitions are ranged and follow the theory of symbolic automata. They are well integrated with regular expressions and Glushkov's construction. They allow for more efficient squaring and subset construction. Instead of being an ad-hoc feature, they are well integrated everywhere.

- OpenFst has no built-in support for regular expression and it was added only later in form of Thrax grammars, that aren't much more than another API for calling library functions. In Solomonoff the regular expressions are the library. Instead of having separate procedures for union, concatenation and Kleene closure, there is only one procedure that takes arbitrary regular expression and compiles it in batch. This way everything works much faster, doesn't lead to introduction of any ε-transitions (in Solomonoff, ε-transitions aren't even implemented, because they were never needed thanks to Glushkov's construction). This leads to significant differences in performance. You can see benchmarks below.

- Many operations are implemented in "better" way. For example

  - Solomonoff has no need for ArcSort because all arcs are always sorted

  - Solomonoff has no Optimise because compiler decides much better when to optimise things

  - Solomonoff has no RmEpsilon, because it has no epsilons in the first place

  - Solomonoff has no CDRewrite because the same effect can be achieved much more efficeintly with lexicographic weights and Kleene closure.

  - In OpenFST if you perform `("a":"b"):"c"` you get as a result `"b":"c"`. OpenFST treats : as a binary operation. Solomonoff on the other hand treats : as unary operation. `("a":"b"):"c"` results in `"a":"bc"`. In fact `:'b'` is treated as `'':'b'` and `'a':'b'` is merely a syntactic sugar for 'a' '':'b'. You can write for example :'b' 'a'. The strings prefixed with : are the output strings, whereas strings without : are the input strings. You can very easily perform inversion of automaton by turning input strings into output strings and vice-versa. For example in Thrax you have `Inverse["a":"b"]` which results in `"b":"a"`. In Solomonoff the inverse of `'a':'b'` becomes `:'a' 'b'`. Very stright-forward. The semantics of `:` in OpenFST strip the output of the left-hand side. In fact, `X:Y` in OpenFST translates more literally to `stripOutput[X]:Y` in Solomonoff.

  - Thrax supports so called "temporary"/"outside of alphabet" symbols. Any time you write `"[NEW_SYMBOL]"` it will take some large UNICODE codepoint hoping that it's not used anywhere else. In Solomonoff this is not necessary, because using type system is much better suited for this task. You can just write

    
        x = 'abcd' // some regex
        x <: [a-z]* //ensure that it uses specific alphabet
        z = x <404> x // use codepoint 404 as some "external symbol"
        z <: ([a-z]|<404>)*
   
       Opis celu powstania projektu powinien w szczególności odpowiadać na następujące pytania:

- Solomonoff is much fater. Results of benchmarks on a large linguistic dictionary are as follows. Thrax compiles in 19 minutes, while Solomonoff in just 4 seconds. OpenFST executes in 250 milliseconds, while Solomonoff in 5 milliseconds. FAR file takes up 27M while Solomonoff's archive only 552K. OpenFST takes up 6336K in RAM, whole Solomonoff only 738K. OpenFST is written in C++, while Solomonoff in Java, so our implementation performs better despite being disadvantaged.

The project found approval among members of Samsung's R&D team for Bixby developement and inductive inference researchers from Dortmund Technical University, Germany. 

3. Rynek (min. 3 konkurencyjne produkty)

Currently there exists only one serious alternative, which is openfst library with their Thrax extension for writing regex-like grammars. Their solution has numerous problems. It's focus on probabilistic approach to modeling nondeterminism, made the library quite slow. It also became a double-edged sword, by making rule-based system difficult to maintain (compiler doesn't warn programmer when nondeterminism causes some rules to overshadow others). Compilation of grammars is lacking in many aspects. The grammar expression language is very basic and obscure. Compiler is not parallized and highly inefficient. On top of that, the probabilistic approach.

Our solution completely gets rid of nondeterminism. We will not attempt to model any probabilistic models. We will focus more heavily on making the expression language user-friendly and helpful in detecting potential non-determinism. The compiler should be able to process multiple rules in parallel to make compilation time faster. We could also take advantage of guarantees of determinism. There are many optimisations to be made thanks to this. The end goal is to make the whole system work in linear time and linear space.


For better user experience and easier management of code, we add build system and basic package manager (although, we don't provide centralised package repository)

Our project has been noticed by other researchers. We will work together with Dortmund University and make Solomonoff publicly available.


There used to be another similar project, developed by AT&T but it's been long discontinued and replaced by OpenFST. Aside from that, the market is extremely niche. There do not exist any other tools (or at least, they are not available publicly). The closest other competitors might include general-purpose automata libraries like Google's RE2 or  Anders Møller's BRICS library. However, those projects are fundamentally different as they implement classical automata instead of tranasducers.



4. Opis produktu (min. 3 moduły/epiki)

A simple and efficient library written in C will be the main and primary component of our product. On top of that, it will have command-line interface equipped with compiler. For easy and quick access, we should support online repl for all curious people who want to give our library a try. The compiler should support parallelism, warn user about non-determinism and allow for possibly some extent of generic programming (by defining functions working on regular expressions or bulk-generation of rules according to some regularities). We should ,however pay extra attention, to not making this language turing complete/undecidable by accident (otherwise compilation might never end).

- simple and efficient library written in Java
  - essential functions for operations of
    - concatenation
    - Kleene closure
    - union
    - composition
    - projection
  - additional less important operations
    - inverse
    - composition
  - algorithms of inference
  - type system
  - integration with LearnLib
  - is optimised for functional ranged transducers (so called symbolic automata)
  - REPL and build system
    - support for parallelism
    - non-determinism warnings
    - packaging system
    - dependency resolver
    - supports everything that compiler does
    - additional directives
  - online repl
    - can write regular expressions on-the-fly
    - can test for determinism without constructing automata (it's more efficient)
    - user can download effects of their work for their local computer

Proposed architecture (one of possible ways we could implement it):

  - there is all theoretical work and background written in our PDF
  - theoretical paper serves as basis for formal specification of library functions
  - Java compiler - everything can be done from regualr expressions. User does not need to write a single Java line to use the compiler.
  - REPL is extensions of compiler itself and shares codebase
  - build system is developed and shipped independently from compiler
package manager is intergrated with build system and shares common codebase
  - online REPL is built by compiling Java compiler with JWebAssembly 
  - backend in Spring
  - website with basic info, documentation, examples and tutorials
YouTube channel and blog contain additional resources. They help us to promote the library and attract users.

Our target audiences include:

- researchers who want to:
  - have some ready-made library with functionalities they need for experiments.
  - verify formal properties of complex sequential systems
- linguists
  - working on rule-based translation
- machine-learning experts
  - who work in fields related to natural language processing
who use Solomonoff inference
  - Companies developing artifical inteligence systems
who might use it as one of their tools. (Especially if their employees are any of the people above)


5. Zakres i ograniczenia


Time is our most valuable resource. If we start running out of it, we might drop support for formal specification and/or transducers. By the end of semester we should have working library, although there is no guarantee that it will be optimised. Optimisations should be ready by the end of second semester, though. There should also be a working basic version of expression language and compiler for it by the end of first semester. We should also have more-or-less working prototype of online repl, although the extent of what "working" means depends heavily on state of library.

Work schedule: 

- first semester
  - formal specification
  - C library prototype (unoptimised)
  - compiler prototype
  - online repl prototype (with dummy compiler functionality)
- second semester
  - optimised Java compiler
  - compiler usable in practice and tested on real life users
  - online repl integrated with compiler
  - machine learning algorithms
  - build system
  - packaging system

Team:

- Aleksander Mendoza
  - formal specification and theoretical foundations
  - compiler implementation
- Bogdan Bondar
  - web design
  - backend development
- Marcin Jabłoński
  - build system
  - REPL
  - assisting with compiler implementation
