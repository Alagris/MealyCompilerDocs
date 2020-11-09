
# Dokument wizji projektu MealyCompiler
#### (MealyCompiler project vision)


Autor: Aleksander Mendoza, Bogdan Bondar, Marcin Jabłoński

Data: 18 March 2020

### 1. Wprowadzenie/Introduction

##### Some theoretical background in nutshell
The foundation of modern technology lies in computability theory. There've been proposed dozens of various computation models. Chomsky proposed entire hierarchy of them. However, the more powerful a model is, the more complex are its properties, which makes it difficult or impossible to perform various operations. For instance you can easily minimize finite state automata, but doing so for non-deterministic automata is NP-hard*, while minimization of Turing machines is undecidable. Our product will focus on special model called Mealy automata. We should take advantage of all guarantees and features this model provides. Thanks to their ability to relate some strings to others, transducers are especially heavily used in natural language processing, machine learning and formal specification of systems. The basic idea behind all kinds of Mealy machines is extending finite state automata with output. Each edge should have 2 labels: one for input and one for output. One of thme decides where to go, the other tells what to print. Such model has benefit of most of the properties of standard finite state automata, while also has many additional properties. You can compose and invert automata very much like functions or relations in other fields of mathematics. It's possible to extend regular expressions with output as well. You can minimize them easily or add non-determinism.

##### Our better model

We should specifically focus only on transducers that represent functions (always produce only one output), while also try to give them maximal expressive power that's practically possible. It should introduce a great model that any machine-learning specialist could add to their toolbox. Every formal-verification reasearcher could also express more advanced system properties, without sacrificing strong guarantees of deterministic models. On top of that, every linguist working with rule-based translation could easily use our product.

*actually it's PSpace, which is conjectured to be NP-hard.

### 2. Cel/Goal

Our compiler of transducers addresses two practical problems: 

- difficulty of maintaining large rule-based systems
- efficiency of evaluating millions of rules in production environment




### 3. Rynek/Market

Currently there exists only one serious alternative, which is openfst library with their Thrax extension for writing regex-like grammars. Their solution has numerous problems. It's focus on probabilistic approach to modeling nondeterminism, made the library quite slow. It also became a double-edged sword, by making rule-based system difficult to maintain (compiler doesn't warn programmer when nondeterminism causes some rules to overshadow others). Compilation of grammars is lacking in many aspects. The grammar expression language is very basic and obscure. Compiler is not parallized and highly inefficient. On top of that, the probabilistic approach

Our solution completely gets rid of nondeterminism. We will not attempt to model any probabilistic models. We will focus more heavily on making the expression language user-friendly and helpful in detecting potential non-determinism. The compiler should be able to process multiple rules in parallel to make compilation time faster. We could also take advantage of guarantees of determinism. There are many optimisations to be made thanks to this. The end goal is to make the whole system work in linear time and linear space.

For better support of machine-learning we might add built-in Mealy inference algorithms.

For better support of formal verification we might add type system.

For better user experience and easier management of code, we add build system and basic package manager (although, we don't provide centralised package repository)

Our project has been noticed by other researchers. We will work together with Dortmund University and make Solomonoff publicly available. 

### 4. Użytkownicy/Audiences

Our target audiences include:

- researchers who want to:
  - have some ready-made library with functionalities they need for experiments.
  - verify formal properties of complex sequential systems
- linguists 
  - working on rule-based translation
- machine-learning experts
  - who work in fields related to natural language processing
  - who use Solomonoff inference 
- Companies developing artifical inteligence systems
  - who might use it as one of their tools. (Especially if their employees are any of the people above) 





### 5. Opis produktu/Description

A simple and efficient library written in C will be the main and primary component of our product. On top of that, it will have command-line interface equipped with compiler. For easy and quick access, we should support online repl for all curious people who want to give our library a try. The compiler should support parallelism, warn user about non-determinism and allow for possibly some extent of generic programming (by defining functions working on regular expressions or bulk-generation of rules according to some regularities). We should ,however pay extra attention, to not making this language turing complete/undecidable by accident (otherwise compilation might never end).

* simple and efficient library written in Java
  * essential functions for operations of
     * concatenation
     * Kleene closure
     * union
     * composition
     * projection
  * additional less important operations
     * inverse
     * composition
  * algorithms of  inference
  * type system
  * integration with LearnLib
  * is optimised for functional ranged transducers
* REPL and build system
  * support for parallelism
  * non-determinism warnings
  * packageing system
  * dependency resolver
  * supports everything that compiler does
  * additional directives
* online repl
  * can write regular expressions on-the-fly
  * can test for determinism without constructing automata (it's more efficient)
  * user can download effects of their work for their local computer

Proposed architecture (one of possible ways we could implement it):

- there is all theoretical work and background written in our PDF
- theoretical paper serves as basis for formal specification of library functions
- Java compiler  - everything can be done from regualr expressions. User does not need to write a single Java line to use the compiler.
- REPL is extensions of compiler itself and shares codebase
- build sytsme is developed and  shipped independently from compiler
- package manager is intergrated with build system and shares common codebase
- online REPL is built by compiling Java compiler with JWebAssembly
       - everything runs on front-end. Because the goal is to be efficent, we should be able to pack everything in thin WebAssembly. No back-end required so we can put it on GitHub Pages.
       - interface is on front-end but compiler is in back-end. We need to find hosting.
- website with basic info, documentation, examples and tutorials
- YouTube channel and blog contain additional resources. They help us to promote the library and attract users




### 6. Zakres i ograniczenia/scope and limitations

Time is our most valuable resource. If we start running out of it, we might drop support for formal specification and/or Mealy inference. By the end of semester we should have working library, although there is no guarantee that it will be optimised. Optimisations should be ready by the end of second semester, 
though. There should also be a working basic version of expression language and compiler for it by the end of first semester. We should also have more-or-less working prototype of online repl, although the extent of what "working" means depends heavily on state of library.  

We propose to split our work into alpha and beta phases:

- alpha includes:
  - formal specification
  - C library prototype (unoptimised)
  - compiler prototype
  - online repl prototype (with dummy compiler functionality)
- beta includes:
  - optimised Java compiler
  - compiler usable in practice and tested on real life users
  - online repl integrated with compiler
  - machine learning algorithms
  - build system
  - packaging system