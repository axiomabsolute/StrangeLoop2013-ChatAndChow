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
    * On the other hand, program fully type check -> type system is a limit to expressiveness
10.  Quick example of limiting expressiveness, tuple problem
    * Tuple: immutable, fixed sized collection of elements, where each element can have a different type.
    * (float, float) -> 2d vector
    * (string, string, string) -> (host, pathname, queryString)
    * Data table joins; not always a good class
    * Problem?
    * 8 different classes, tuples 1-7 elems, + special
    * 8 constructors.
    * We don't have this for Lists or Maps. Something's wrong
11. Tuples nest after 7 elements
    * Accessor syntax gross
    * We don't have this for Lists/Maps; what gives?
12. Problem: Variable number of type args because heterogeneous
    * To keep type safety, we have to be able to associate the appropriate type with the argument in each position, which most languages can't do.
    * Luckily, there's a way around.  Take an array of Type objects as the first argument, and an array of values as the second, hen cast each item as it's put in and out...
    * Completely lost type safety.
    * Number of types and args don't match
    * Type of an arg doesn't match
    * Out of bounds
    * These are all runtime check!
    * Uses escape hatches to bypass type system
13. If you think it's just Tuples and you can avoid it, think again.  Func, Action, this time with up to 16 elements!
    * Why so many elements?
    * Used to represent anonymous functions, which are often generated code and can get very long.
    * People actually run into this problem sometimes with generated code.
    * It's very confusing when it happens
14. Martin odersky's talk; language landscape
    * Map of how strongly guarantees, and what problems can be expressed
    * C#/Java 5 in the dead middle.
    * LL C; weak; bitmangling for good and ill
    * Go, Java 4; strong system, but can't express all problems.  My way or highway
    * Over last years, focus shift up
    * TypeScript, Dart, "gradual typing"; one big escape hatch.  Clojure moving here with core.typed
    * Finally, type to the max; Much more powerful type systems
    * what do you mean?
15. WARNING
    * Bad rap; complexity, not undeserved
    * Golden goose, dream
    * If it compiles, it runs without error.
    * (Mostly... still escape hatches)
    * Type checker picky.  Curse it.  Mock you
    * Ugly type signatures & error messages
    * Scala fixing with 90% signatures and smarter type debugger
16. Lastly, you get statements like these
17. KIND OF a joke
    * Type theory is complicated
    * Based on very abstract math; Category theory (uber abstract algebra)
    * Myth of the "aha" moment
    * As soon as you understand them, can't explain anymore
    * Like talking to an enlightened buddhist monk
    * Sounds like they're not really saying anything
    * Alright, so what does this complexity get us
18. NPE's suck
19. Get rid of em!
20. Nulls, the billion dollar mistake
    * Often have possibility of failure in the system, which we represent by null
    * e.g. converting "23" to 23
    * NPE at runtime; type system fail
21. Introducing option type
    * Imagine instead that your language simply doesn't allow values to be null
    * All values either concretely initialized
    * Or represented by option type
    * Option: two possible values, Some of your type, or special None
    * Looks a lot like null, but...
    * Now it's compile time error
22. Let's pretend we don't know that `res2` is `None` at compile time
    * Have to add these `.get` calls to get the wrapped type
    * If we do this without first checking if each result is empty, it is a _compiler error_
    * Works, but ugly.
    * Looks a lot like null checks...
    * C#/Java static code analysis tools could do this
23. Option Monad
    * Remember that monoid functor garbage?
    * That's this guy
    * Monads let you define boilerplate behavior that should happen between steps
    * In this case, that's the `if(None) print return` behavior
    * Yield says "if any part is `None`, the whole thing is `None`."
24. Otherwise, carry on.
    * The point is, this behavior is user definable.
    * In languages that support monads, you could have it *assume* None values are 0 and just carry on with the computation (if, say, you're summing things and want to ignore missing values)
    * Or that None values are 1 (if you're multiplying)
25. Monads can do other stuff. This one is in F#
    * Normal code, except async {} and let!.  let! is the magic await
    * Allows us to run multiple web requests in parallel and hook up callbacks behind the scenes
    * Here's secret; .NET has had monads for awhile
    * Precursor to C# async/await, stolen from F#
    * LINQ, the lazy evaluation monad
    * MS is chosing to adopt individual monads under syntax sugar to make them more approachable.  async/await, LINQ, Rx are all "monadic" libraries.
    * But this is a compromise
    * Each monad is separate syntax in C#, because they didn't adopt a general syntax to allows users to build their own monads
    * You CAN overload LINQ in C# to do this, but its confusing
26. Monads are old news
27. Dependent types are the bees knees.
    * Part of the tuple problem was bound access
    * Same thing here, with lists
    * Define a generic list type, create some lists of integers and add them up pairwise
    * Add lists of different size, runtime error -> type system failure
28. Dependent types come to save the day
    * Like generics, but add the ability to provide *values* as generic type parameters, and do normal operations on those values
    * Here, we add a dependent type, listLength
    * When we do pairwise add, we expect the new list to have the same length
    * Now size-mismatch is a compile time error
29. You could also use this for list concatenation, using operations on the dependent type
    * `public MyList<A, listLength+listLength2 concat(MyList<A, listLength2> other)`
    * Resource state changes
    * Not going to show
    * Idris/Agda dependent types, Plaid typestate
30. Back to the tuple problem
31. It's still here
    * No good solution yet, but dependent types are a step
    * Oddly, C++ and typed lisps come closet with templates/macros
    * Keep compile time type safety, but huge impact on compile times
    * Still count this as an escape hatch
32. What does clojure say about all this?
    * Sure you get free checks, but they offer at best a false assurance
    * Type system simply cannot catch everything, so why bother?
    * Unit tests!
    * Leaving out the type system greatly reduces barrier to understanding code
    * focus on logic and tests
33. Read the quote
34. This guy made nulls; billion dollar mistake
35. Not sure I trust him
    * If I had a time machine...
36. Alan Kay agrees
37. What's my point?
38. Regardless of whether you're a fan of static typing or not, it's clear there's a lot of research being done in this area
39. New advances are making it easier to introduce typing slowly, and expanding expressiveness of type system
    * Elegant, flexible solutions
40. It's easy to grind yourself into a rut and forget to look at new advances, because they're hard
    * Just as easy to fall in love with a shiny new language that solves superficial problems
    * Keep your eye out on new languages
    * Sneaking into languages like C#
    * When you see a new language, look for the core principles beneath the chrome

41. This is what my year and a half long journey getting to StrangeLoop has been about
    * Learning as much as I can about a very basic component to the tools I use every day in my job; Types.
