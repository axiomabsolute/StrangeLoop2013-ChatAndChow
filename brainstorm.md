* Null by default vs no-nulls; nulibility
* Semantics built into the language vs built IN the language; Monads
* Step between generics and generics 2.0; value types, or dependent typing
* Types can change; typestate programming ('checked') and structural/implicit types ('unchecked')
* Types are for communicating with the compiler
* If your program fails at runtime without you explicitly telling it to, the compiler has failed
* Unit tests should only check semantics (does it do what you expect), not correctness (does it work)
* We're wasting our time solving the wrong problems
* We're not advancing because we waste time on little problems
* A language is powerful if you can implement changes in the language, not as an extension
* Types influence the langauge from the ground up; what native code gets produced all the way up to the tools and documentation
* Types influence the ecosystem around the language; tooling, libraries, documentation
* Types can get in the way w/ verbosity
* Types stop being useful when you can't specify a generalization in the system
* Escape hatches are necessary and useful, but should be minimized
* Types let you forget about things when you're brainstorming/prototyping
* Dynamic types are essentially one big escape hatch.  Formal types are DERIVED by the JIT
* Tuple/Func/Action problem
* Null problem
* 

## Messages

1. The type systems of the current popular programming languages are insufficient

* Rise in Dynamic languages was the first sign
* TDD was the next
* Current language research is addressing this

2. Insufficient type systems lead to wasted effort

* How many NPEs have you fixed?
* How many dangling resources?
* How many times have you had to look at documentation for something?

3. Types translate runtime errors into compile-time errors

* The goal of the type system should be to eliminate as many runtime errors as possible, by encoding them as types

4. Types are the programmer's only communication with the compiler

* Even in dynamically typed languages, performance is only achieved through JIT compilers, which rely on predicting runtime types
* Require coding in a not-dynamic style for performance (consistent, inflexible objects allow prediction)
* Tooling (autocomplete, suggestions, etc) are really about types too
