#Dokument wizji projektu MealyCompiler

Autor: ...

Data: ...

### 1. Wprowadzenie/Introduction

The foundation of modern technology lies in computability theory. There've been proposed dozens of various computation models. The most popular of them being Turing machines, unrestricted register machines, recursive functions, lambda calculus, cellular automata, circuit systems, algorithmic state machines etc. There are also many less powerful and specialized models such as primitive recursive functions, memory-restricted Turing machines, simply-typed lambda calculus, context-free grammars, determinisitc pushdown automata, finite state automata, regular expressions and many more. All of them (and many variantsof them) found extensive applications in industry. One of the models, called Mealy machines is especially heavily used in natural language processing, machine learning and formal specification of systems.

> Preatty neet, i like it but too bloated IMHO
> I would suggest to make it more like marketing gibberish than introduction to serious papers. Maybe something more like following 

A complex solution designed for NLP, ML and formal specification. Our product is based on a Mealy machine which is a highly specialised computation model.

> But it's only my opinion and i understand if you not share my point

### 2. Cel/Goal

Our compiler of Mealy machines addresses two practical problems: 

- difficulty of maintaining large rule-based systems
- efficiency of evaluating millions of rules

> no comments

### 3. Rynek/Market

Currently there exists only one serious alternative, which is openfst library with their Thrax extension for writing regex-like grammars. Their solution has numerous problems. It's focus on probabilistic approach to modeling nondeterminism, made the library quite slow. It also became a double-edged sword, by making rule-based system difficult to maintain (compiler doesn't warn programmer when nondeterminism causes some rules to overshadow others). Compilation of grammars is lacking in many aspects. The grammar expression language is very basic and obscure. Compiler is not parallized and highly inefficient. On top of that, the probabilistic approach

Our solution completely gets rid of nondeterminism. We will not attempt to model any probabilistic models. We will focus more heavily on making the expression language user-friendly and helpful in detecting potential non-determinism. The compiler should be able to process multiple rules in parallel to make compilation time faster. We could also take advantage of guarantees of determinism. There are many optimisations to be made thanks to this. The end goal is to make the whole system work in linear time and linear space.

For better support of machine-learning we might add built-in Mealy inference algorithms.

For better support of formal verification we might add temporal logic SAT-solver and specificaion meta-language.

> no comments

### 4. Użytkownicy/Audiences

Our target audience includes researchers, linguists and machine-learning experts working in fields related to natural language processing. Companies developing artifical inteligence systems might use it as one of their tools. 

> no commnets

### 5. Opis produktu/Description

A simple and efficient library written in C will be the main and primary component of our product. On top of that, it will have command-line interface equipped with compiler. For easy and quick access, we should support online repl for all curious people who want to give our library a try. The compiler should support parallelism, warn user about non-determinism and allow for possibly some extent of generic programming (by defining functions working on regular expressions or bulk-generation of rules according to some regularities). We should ,however pay extra attention, to not making this language turing complete/undecidable by accident (otherwise compilation might never end).

>I would rather make it a little bit simpler

* simple and efficient library written in C
  * ports for other languages
* compiler and CLI
  * support for parallelism
  * warnings
  * API for developers
* online repl

### 6. Zakres i ograniczenia/scope and limitations

Time is our most valuable resource. If we start running out of it, we might drop support for formal specification and/or Mealy inference. By the end of semester we should have working library, although there is no guarantee that it will be optimised. Optimisations should be ready by the end of second semester, 
though. There should also be a working basic version of expression language and compiler for it by the end of first semester. We should also have more-or-less working prototype of online repl, although the extent of what "working" means depends heavily on state of library.  

> no comments
