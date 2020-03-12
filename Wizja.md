#Dokument wizji projektu MealyCompiler

Autor: ...

Data: ...

### 1. Wprowadzenie/Introduction
>Dokument dotyczy projektu realizowanego w ramach  Niniejszy dokument służy przedstawieniu przeznaczenia tworzonego systemu, jego głównych cech i przyjętych założeń.

The foundation of modern technology lies in computability theory. There've been proposed dozens of various computation models. The most popular of them being Turing machines, unrestricted register machines, recursive functions, lambda calculus, cellular automata, circuit systems, algorithmic state machines etc. There are also many less powerful and specialized models such as primitive recursive functions, memory-restricted Turing machines, simply-typed lambda calculus, context-free grammars, determinisitc pushdown automata, finite state automata, regular expressions and many more. All of them (and many variantsof them) found extensive applications in industry. One of the models, called Mealy machines is especially heavily used in natural language processing, machine learning and formal specification of systems.

### 2. Cel/Goal
>Należy opisać, jaki problem zostanie rozwiązany dzięki projektowi, po co właśnie taki temat podejmujemy.
Na przykład:
Celem projektu jest stworzenie nowego serwisu społecznościowego “RetroCar”, umożliwiającego zawieranie znajomości i wymianę informacji osobom z Polski, zainteresowanym starymi samochodami.

Our compiler of Mealy machines addresses two practical problems: 

- difficulty of maintaining large rule-based systems
- efficiency of evaluating millions of rules




### 3. Rynek/Market
>Należy odnieść się do dostępnych rozwiązań realizujących podobny cel. Powinno być jasne, w jakim zakresie tworzony system się od nich odróżnia.
Na przykład:
Serwis “RetroCar”, w odróżnieniu od istniejących serwisów poświęconych wybranym markom samochodów (np. http://www.syrena.nekla.pl/), umożliwi zrzeszanie wielbicieli dowolnych marek samochodów. Jednocześnie będzie pozwalał, w miarę możliwości technicznych, na import danych z innych serwisów, na przykład poprzez mechanizm RSS.

Currently there exists only one serious alternative, which is openfst library with their Thrax extension for writing regex-like grammars. Their solution has numerous problems. It's focus on probabilistic approach to modeling nondeterminism, made the library quite slow. It also became a double-edged sword, by making rule-based system difficult to maintain (compiler doesn't warn programmer when nondeterminism causes some rules to overshadow others). Compilation of grammars is lacking in many aspects. The grammar expression language is very basic and obscure. Compiler is not parallized and highly inefficient. On top of that, the probabilistic approach

Our solution completely gets rid of nondeterminism. We will not attempt to model any probabilistic models. We will focus more heavily on making the expression language user-friendly and helpful in detecting potential non-determinism. The compiler should be able to process multiple rules in parallel to make compilation time faster. We could also take advantage of guarantees of determinism. There are many optimisations to be made thanks to this. The end goal is to make the whole system work in linear time and linear space.

For better support of machine-learning we might add built-in Mealy inference algorithms.

For better support of formal verification we might add temporal logic SAT-solver and specificaion meta-language.



### 4. Użytkownicy/Audiences
>Należy opisać, do jakich użytkowników będzie skierowany serwis—określić zarówno ich potrzeby jak i stopień zaawansowania w obsłudze systemów informatycznych.
Na przykład:
Serwis “RetroCar” jest kierowany do użytkowników, którzy chcą pochwalić się swoim samochodem, zasięgnąć porady innych użytkowników oraz zawierać znajomości. Użytkownicy potrafią posługiwać się systemami typu forum dyskusyjne, galeria zdjęć czy blog.

Our target audience includes researchers, linguists and machine-learning experts working in fields related to natural language processing. Companies developing artifical inteligence systems might use it as one of their tools. 



### 5. Opis produktu/Description
>Należy wymienić (można w punktach) główne funkcjonalności oferowane przez tworzony system. Należy zaznaczyć, które z nich wyróżniają się na rynku dostępnych rozwiązań.
Na przykład:
zakładanie profilu użytkownika z możliwością wgrania avatara, określenia zakresu widoczności poszczególnych danych osobowych
zakładanie profili posiadanych samochodów—większość serwisów motoryzacyjnych umożliwia podanie tylko jednego pojazdu
galeria zdjęć
tagowanie zdjęć i wyszukiwanie po tagach—serwisy motoryzacyjne oparte o prosty silnik forum na ogół nie mają takich możliwości
opcja importu zdjęć z wybranych serwisów foto, na przykład flickr
prowadzenie dziennika internetowego lub import wiadomości użytkownika przez rss z innego serwisu
łatwo przeszukiwalna baza wiedzy na temat rozwiązywania różnych problemów związanych z samochodami, edytowana przez użytkowników—w wielu serwisach porady giną pośród wielu wątków na forum i użytkownicy zadają wciąż te same pytania
uczestniczenie w dyskusjach na forum, możliwość personalizacji stopki
możliwość wysyłania prywatnych wiadomości innym użytkownikom
możliwość dokumentowania zlotów motoryzacyjnych – wgrywanie opisów, zdjęć, oznaczanie uczestnictwa – dostępne serwisy nie umożliwiają łatwego organizowania tego typu informacji
możliwość tworzenia grup użytkowników, na przykład zainteresowanych daną marką samochodów, odnawianiem starych pojazdów czy wyścigami
organizowanie konkursów z głosowaniem na samochód miesiąca
branżowa książka adresowa warsztatów mechanicznych, lakierników, wulkanizatorów, ... z łatwym wyszukiwaniem, dopisywaniem komentarzy, lokalizacją na mapie i integracją z dostępnymi w sieci źródłami takich danych—w wielu serwisach organizacja tego typu danych pozostawia wiele do życzenia, trudno odnaleźć poszukiwanych fachowców

A simple and efficient library written in C will be the main and primary component of our product. On top of that, it will have command-line interface equipped with compiler. For easy and quick access, we should support online repl for all curious people who want to give our library a try. The compiler should support parallelism, warn user about non-determinism and allow for possibly some extent of generic programming (by defining functions working on regular expressions or bulk-generation of rules according to some regularities). We should ,however pay extra attention, to not making this language turing complete/undecidable by accident (otherwise compilation might never end).

### 6. Zakres i ograniczenia/scope and limitations
>Należy przedstawić zakres projektu obowiązujący przy pierwszej wersji systemu (na zaliczenie). Jeśli przewidujemy istotne ograniczenia, również powinny się tu znaleźć.
Na przykład:
W pierwszej wersji systemu możliwa będzie edycja profilu użytkownika, dyskusje na forum, tworzenie galerii i edycja branżowej książki adresowej. System będzie wprowadzał ograniczenia na ilość wgrywanych multimediów.

Time is our most valuable resource. If we start running out of it, we might drop support for formal specification and/or Mealy inference. By the end of semester we should have working library, although there is no guarantee that it will be optimised. Optimisations should be ready by the end of second semester, 
though. There should also be a working basic version of expression language and compiler for it by the end of first semester. We should also have more-or-less working prototype of online repl, although the extent of what "working" means depends heavily on state of library.  