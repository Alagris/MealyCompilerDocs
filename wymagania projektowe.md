Dokument wizji projektu

Nazwa projektu: Solomonoff

Autorzy: Aleksander Mendoza, Bogdan Bondar, Marcin Jabłoński

Data: 13.12.2020

#### 0\. Wersje dokumentu

- 13.12.2020 - initial version

#### 1\. Elementy składowe projektu (produkty projektu)

Należy jednoznacznie i precyzyjnie określić wszystkie powstałe w ramach projektu elementy programistyczne i udokumentowane nieprogramistyczne elementy projektu. Przykładami elementów programistycznych są:

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
    - has all features of the compiler itself
    - user can download effects of their work for their local computer
    - syntax highlighting
    - documentation and code samples
- theory and specification
    - scientific papers explaining the theory with appropriate mathematical rigour

#### 2\. Granice projektu

There are not many limitations in our project. It does not require keeping track of userbase, by using Java we do not impose any restrictions on operating systems and most importantly, we support most of the required features. Some users might feel restricted by not being able to define nondeterministic transducers but in reality it's for the better. Solomonoff has certain restrictions, that are there by design and in practice, they should not be a major issue. We do not support probabilistic transducers, but it's because probabilities do not play well with manually crafted regular expressions and they may lead to unstable solutions in the long term. Solomonoff also hides most of its API from user. Only very minimalist Java methods are exposed and transducers should not be manipulated programmatically. This also is by design, because Solomonoff puts heavy emphasis on the language of regular expressions. It embeds regex in a special vernacular language that more than compensates lack of programmatic API. It also makes the system more user friendly as a whole.

#### 3\. Lista wymagań funkcjonalnych

- basic useage via regular expressions: union, concatenation, kleene closure, composition, inversion
- advanced usage via extensibility and native functions: Glushkovs construction supports calls to extenal functions
- ease of setup and efficient compilation: easy to use build system
- user firendly REPL from web browser without any required setup: compiler integrated in form of a library used by Spring backend


#### 4\. Lista wymagań niefunkcjonalnych

- scientific papers describing the theory in detail
- end user tests


#### 5\. Mierzalne wskaźniki wdrożeniowe

- efficiency benchmarks on large datasets of regular expressions
	- RAM usage
	- disk usage 
	- execution speed
	- compilation speed
- parallel compilation 
- installable tarball avaiable for download 
- unit tests


#### 6\. Kryteria akceptacji projektu dla I semestru prac

- basic regular expressions: union, concatenation, kleene closure
- basic online playground with syntax highlighter and WebAssembly
- prototype of type system and  weighted automata

#### 7\. Kryteria akceptacji projektu dla II semestru prac

- extended regular expressions
- optimised compiler
- inductive inference algorithms
- build system
- online playground with backend, docs, samples and tutorials

#### 8\. Organizacja pracy zespołu

- Aleksander Mendoza
  - Glushkov's construction 
  - weighted transducers
  - inductive inference
  - nondeterministic minimization
- Bogdan Bondar
  - backend
  - frontend
  - compiler integration
- Marcin Jabłoński
  - build system
  - repl
  - dependency resolver

Aleksander Mendoza is responsible for finding clients and communicating with them. 

Tools:
- JIRA
- git
- GitHub

#### 9\. Ryzyka projektowe

The most important risk of our project was its heavy reliance on advanced theoretical concepts. It required plenty of rigour to make sure our foundations are correct and well defined. Should anything in our understanding of automata be wrong, the whole project would at risk of becoming irrelevant. 

The second most critical concern was time. There was plenty to do and very little time. It was haard to estimate how much time any of the tasks would take. While missing initial deadlines due to unforseen complications is typical for software engineering projects, our project was exposed to a such risks at a much larger scale. Should anything be wrong in the formal specification, it could require months of additional research. In the worst case, if there was a mistake, some goals might turn out to be mathematically impossible. For this reason our team had to be rigorous about their promises.

There was little risk with respect to technologies, although the most significant one was chosing the appropriate infrastructure for an open-source non-profit project. We can't bear large costs of maintenance, therefore we used open-source and free resources as much as possible. While in the end the project had to switch from WebAssembly to using backend, we hope that in the long-trem we will find hosting sponsored by some research institution. In the worst case, should we not get any sponsorship, the most of the project is resilient and can still remain relevant even without backend. The web interface could be then treated as an optional addition, that user can download and run locally as an alternative to terminal-based interface.

#### 10\. Kamienie milowe

- proof of concept and first implementation of Glushkov's construction
- proof of concept for type system
- establishing relations with Dortmund University
- preparing code for adoption in Samsung (requires writing a very specific feature that allows for converting legacy codebase from Thrax to Solomonoff)
- getting build system ready
- testing 

