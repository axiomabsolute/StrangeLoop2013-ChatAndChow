1. StrangeLoop
    * Forefront
2. Basically OSS leaders and internet trends
3. Lots of cool techs
4. Not going to talk about those
    * instead, why I got interested in SL
3. Types
    * Programming lang design
4. These two guys
5. Language design super heroes
    * Created biggest alternative JVM langs
    * Opposing ideals; Rich Hicky Clojure, Martin Odersky Scala
    * Top 20 on GitHub
6. On the surface, look very different
    * Clojure: dynamic, concise, Lisp
    * Scala: OO to the core, built on top of advanced type system, vaguely Java syntax
7.  But beneath the surface, commonalities
    * Very express
    * Active communities
    * Both built with concurrency in mind
    * Actively used in research and industry
    * Most important similarity: Clear core set of principles, evident throughout entire language
    * Compromise is not a lasting design principle
    * Everyone agree JVM/Java successful
8. But over the last years, creep up on Perl/PHP/JavaScript to be the butt of the language design community jokes.
    * Started out as a series of compromises, continued to compromise
    * Kind of OO, public static void main, but also primitive types
    * Kind of has generics, but Type erasure limits runtime type effectiveness
    * Statically typed, but un-expressive typesystem leaves us with runtime null checks and casting
9. Martin Oderstky's talk about the type problem
    * On one hand, safety, sometimes false assurances
    * On the other hand, program fully type check -> type system is a limit to expressiveness.
10.  Quick example, tuple problem
    * Tuple: immutable, fixed sized collection of elements, where each element can have a different type.
    * (float, float) -> 2d vector
    * (string, string, string) -> (host, pathname, queryString)
    * Data table joins; not always a good class
    * Problem? 8 different classes, 8 constructors.  We don't have this for Lists or Maps. Something's wrong
11. Tuples nest after 7 elements
    * Accessor syntax gross
12. Problem: Variable number of type args because heterogeneous
13. If you think it's just Tuples and you can avoid it, think again.  Func, Action, this time with up to 16 elements!
14. Martin odersky's talk; language landscape
    * Map of how strongly guarantees, and what problems can be expressed
    * C#/Java 5 in the dead middle.
    * LL C; weak; bitmangling for good and ill
    * Go, Java 4; strong system, but can't express all problems.  My way or highway
    * Over last years, focus shift up
    * TypeScript, Dart, "gradual typing"; one big escape hatch
    * Finally, type to the max; Much more powerful type systems
    * what do you mean?
15. WARNING
    * Bad rap; complexity
    * Type checker picky.  Curse it.  Mock you
    * Ugly type signatures & error messages. Scala fixing with 90% signatures
16. Lastly, you get statements like these
17. KIND OF a joke
18. NPE's suck
19. Get rid of em!
20. Nulls lead to runtime errors
21. No more null in your language.
    * Option type has two possible representations; none or wrapper, Some
    * Now it's compile time error
22. Appease with checks
    * Works, but ugly.  Static code analysis tools could do this
23. Monad; remember that monoid functor garbage?
    * Let you redefine <- and yield to do your own thing, in this case, return None if anything is None
24. Otherwise, carry on.
25. Monads can do other stuff. This one is in F#
    * Precursor to C# async/await
    * Normal code, except async {} and let!.  let! is the await
    * Here's secret; .NET has had monads for awhile, hidden in LINQ.  MS is chosing to adopt individual monads under syntax sugar to make them more approachable.  async/await, LINQ, Rx are all "monadic" libraries.
26. Monads are old news
27. Dependent types are the bees knees.

