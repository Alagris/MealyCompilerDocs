# Presentation #0

### About

Our project is aims at creating simple compiler of Mealy automata. User should be able to write code in form of special flavour of regular expressions. Then the compiler should turn it into description of automaton. Because those automata are not Turing-complete it makes little sense to produce executable files. Instead the file will just contains graph structure of automaton and there will be dedicated runtime for executing it (in form of C library with possible bindings).

### Actors

The nature of project inherently doesn't require many actors. There is just user and the library/compiler. User writes code, compiler turns it into automata and library implements runtime required for executing it. No database is required. No admins are necessary. No technical support and no internet access is obligatory.

The only place where it gets a bit more complicated is online repl, but if everything goes ok we might use WebAssembly, make everything work on client-side and post everything on GitHub Pages.

### Functionalities

- compilation
  - user opens file in their favourite editor (we might make some syntax coloring for vim/sublimetext etc)
  - user writes code
  - user saves file
  - user runs compiler
  - compiler accepts and produces file with automaton or rejects and prints error description
- repl
  - user starts up commandline repl
  - (optional) user loads code from file
  - user writes expression and hits enter
  - repl accepts and prints expression result or throws error message
  - (optional) user exports some expression/variable to file in form of compiled automaton
  - user closes repl
- online repl
  - user connects to GitHub Pages and sees repl interface
  - user performs any actions that could be performed in commandline repl
  - user disconnects

### Technology

- library written in C - alternatively we might use Rust but C has one strong advantage over Rust... it's more popular and widespread :'(
- compiler written with help of yacc&bison (probably) - because there is nothing better for C duh
- C verified with ACSL (probably) - this is the standard but there are alternatives such as Coq or Agda. But ACSL is easiest
- online REPL written in vanilla JavaScript & WebAssembly (probably) - better to keep it simple. Moreover getting rid of server-side will allow us not to worry about hosting, and puts the efficiency of our library to a test. 

### Architecture 

Very simple:
- PDF with theoretical background
- C library uses PDF
- compiler uses C library
- repl uses compiler
- repl is compiled to WebAssembly and turned into Javascript library
- Online repl uses javascript library
- and everything is open-source and posted on GitHub with GitHub Pages as hosting
- thanks to ACSL and formal specification no unit tests are necessary (except maybe for online interface)

No server-side, no database, no centralised files storage, no user accounts, no book-keeping of anything at all.

### Roles

- Aleksander-Mendoza (product owner)
   - has contacts to members of NLP department (and they are the most direct clients of the project)
   - writes formal specification 
   - responsible for most of theoretical background
- Marcin Jabłoński (Development team)
   - writes C library
   - implements formal specification
- Bogdan Bondar (Development team)
   - writes web interface
   - creates unit tests

### Challenges

- bring theoretical background to perfection
- educate everyone about automata theory so that all team members can have deep understanding of the roject
- meet practical needs of clients (researchers and linguists). Especially efficiency and flexibility of library
- do it on time