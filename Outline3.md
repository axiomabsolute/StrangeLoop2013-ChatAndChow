1. StrangeLoop

StrangeLoop is a conference for the creators and users of the languages, libraries, tools, and techniques at the forefront of the industry.

Basically its a place for the best and brightest in the OSS community to get together and talk about what they're working on.  It more or less follows the interests trends that go through sites like /r/programming and hackernews.  They drive that content.

2. Emerging Techs

Many of the great technologies that have shaken up the industry have been anounced or demoed early in their lifetime at StrangeLoop.  Projects like Hadoop, Storm, and CoffeeScript enojyed increased community attention and contributions from this limelight.

There were a few cool technologies talked about at StrangeLoop this year, but that's getting a little too close to the topic that Christy and I will be talking about at the annual meeting, so I'm going to stay away from that for now.  What I *will* talk about, however, is how I first got interested in StrangeLoop, and why I went.

3. Types

Programming language design, type theory, and these two guys.

4. My Heroes

These two guys are language design super heroes.  They've created the two biggest alternatvie languages for the JVM, languages with very opposing fundamental ideals; Rich Hicky, with Clojure, and Martin Odersky with Scala.  Both languages are in the top 20 most popular for open source projects on GitHub.

On the surface, these languages couldn't look more different.  Clojure is a dynamic language with a very concise syntax inspired by Lisp, whereas Scala is OO from the ground up, building on an advanced type system with syntax vaguely reminiscent of Java.

But these languages have several similarities beneath the surface.  Both are generally agreed to be very expressive and have active, helpful communities.  Both were built with concurrent and distributed programming in mind. Both are actively used in both research and commercial industries.  But the most important similarity, I think, is that both languages have a very clear set of core principles they adhere to, and those principles are evident throughout the entire language.

5. Compromise is not a lasting design

So, everyone agrees that the JVM and Java have been hugely successful, but over the last decade or so, Java has slowly been creeping up on Perl, PHP, and JavaScript as the butt of the language design community's jokes.  The problem is that Java started out as a series of compromises, and has only evolved into more compromises since.

It's kind of OO, forcing you to wrap even basic programs in a class with a main method, but supports primitive values at the lowest level.  It kind of has generics, but Type erasure limits runtime metaprogramming.  It's statically typed, but the type system is fairly limited in what it can express, and so we're left with runtime null checks and type casting.

6. The Type Problem

Martin Odersky's keynote talk was about what he called the type problem.  On the one hand, static typing provides a safety net to the programmer, catching common errors and giving them some measure of (sometimes false) assurance that they're program is correct.  On the other hand, the whole program must type fully type check, meaning that the type system is in, some sense, a limiting factor on what kinds of solutions the programmer can express; they can only write about things the type checker can handle.

7. Tuple problem

As a quick example of what I mean by the type system "limiting" what kinds of solutions the programmer can express, I found this example in the .NET API; the tuple type.

For those of you who aren't familiar with them, a tuple is an immutable, fixed sized collection of elements, where the element in each position has a specified type.  So you could have a tuple of two real numbers, representing a point in 2D space.  You could have a tuple of three strings representing the host, pathname, and query string in a url.  But you can also use a tuple to represent mixed datatypes, like the return from a database query with arbitrary joins; there may not be a class that cleanly represents the aggregation of the joined data, but by encoding it as a tuple the structure, that is, the order and types in the data, is guaranteed to be consistent.  So they're pretty useful.

So what's the problem?  Notice, there are actually 8 distinct class definitions of the tuple, corresponding to tuples with 1 to 7 different values in the, plus an eighth one that's a little different.  Along with that, there are eight different constructors, one corresponding to each definition.  Something is clearly wrong here.  We don't have a different constructor for every sized list or hashmap we make, and if you want to make a tuple with more than 7 items, you have to nest them, using the special eighth constructor to make something that looks like this!

And then to get data back out, you use this monstrosity!

So what's going on here?  The problem is that, unlike lists, tuples are heterogeneous, that is, they can take multiple types.  That means that in order to keep our type sanity we have to know the type of the element in every position, which means that to define a variable-length constructor we need to take a variable number of type arguments corresponding to each of the arguments in the constructor, which C# has absolutely no way to express.

Luckily, there's a way around this.  Instead of taking in a variable number of type arguments, you take in an array of Types as the first parameter, and then a bunch of arguments of the top type, Object.  Then you cast each item as it's retrieved from the array and.....

You've completely lost type safety.  What happens if the number of types doesn't match the number of arguments?  What happens when Type of an argument doesn't match the one provided in the constructor?  What happens when a user tries to access a value that's outside the bounds of the tuple?

These all get translated into runtime errors, because the type checker doesn't know how to reason about them at compile time.  We've had to use escape-hatches built into the type system to express solutions it can't comprehend.  We've completely abandoned type safety.

And even if you don't like Tuples and vow never to use them again, this pattern shows up again, in Func objects (the things that get created with `(x) => x+2`) and in Action objects.  So somethings wrong.

8. Type Compromise

This is what we mean by compromising in the type system.  In his talk, Odersky showed this graphic showing where languages like Java and C# lie in the world of type systems; dead in the middle, a perfect compromise between how strongly the language guarantees type safety and what kind of problems those guarantees hold for.

In the lower left are C and assembly, which have a very weak notion of type safety and allow bit-mangling for both good and evil designs.  Moving over to the right are langauges like Java pre-generics and Google's new Go programming language.  These languages have very strong type systems, but they're very limited in what they can express, which Odersky calls "my way or the highway" languages.

Over the last several years, however, programming language design has shifted towards the top half of the graph.  In only the last couple of years, the notion of gradual typing, that is, languages which are fundamentally dynamically typed but allow the user to add type annotations at their convenience, have come up.  Languages like TypeScript and Dart, languages which add type systems on top of JavaScript, are essentially one _big_ trap door.  They allow you to finely control which areas of your code are type checked (say, the layer that interacts directly with the database and represents domain entities in your application), and which should not (i.e. tuples made by joins).

Finally, the last category, which attempts to strongly type _everything_.  Languages like Scala and F#, and the langauge Haskell which is heavily used in the research community, have much more complicated and more powerful type systems, capable of expressing much more complicated solutions than those in Java without sacrificing type safety.  What do I mean by that?

9. WARNING

A warning for the faint of heart; these languages have a bad rap for being extremely complicated to use, and I don't think that's entirely overstated.  These languages are after the golden goose, the dream of programmers; if the code compiles, it is without error.  Mostly without error (there are still some escape hatches).

That means that the type checker is even more picky than you're used to.  You will curse it.  It will mock you.

It also means that you'll see some crazy type signatures in the documentation.  This is something that Scala, in particular, is working on by providing "simplified" 90% use case type signatures.  As usual, the devil's in the details.

Lastly, you have to brace yourself for difficult explainations to some problems, often accompanyed by really bad humor trying to make light of the topics.  People will say things like this and expect you to understand.  (I'm almost there)

10. So, what does all this complexity get us?  Null and Monads

Everyone hates NPE's, right?  Let's get rid of them.  Instead, we have a type called Maybe.  Maybe is a wrapper, all it does is hold another another type, or a special constant value, Nothing.

Every time we need a value that may or may not be initialized, it gets wrapped in a Maybe.  And when we try to use it, since it's not just an Integer, but a Maybe<Integer>, we have to check whether it's nothing first.  If we don't, the type checker scolds us.  In return, we're guaranteed to not have NPE's!  But this code is kind of ugly, and we could do something similar with static code analysis in Java and C#!  We're not impressed.

This is where monads come in.  Remember that (not so funny) joke about monads and functors?  That's this guy.  What monads let you do is essentially define some behavior that you want to happen in-between actions in your code.  In this case, we want to get rid of all these checks for Nothings, since they all do the same thing, we really only care if the final result is Nothing, we don't care about the intermediate steps.

So we get somethign that looks kind of like this (made up syntax).

Whats going on is that the monad provides specific meaning to <- in a given context.  In this case, it takes a bunch of values and makes Maybe<Integer>'s out of them.  The monad also provides a special meaning to return, which here translates into "if any argument is Nothing, the whole thing is Nothing".

There.  Only one check for Nothing now, the rest are hidden by the monad.  And we're guaranteed to have no NPE's.  And the world rejoices.

That's why people are so excited about the concept of monads.  They're difficult to explain and define, because they're so general.  This same abstraction can be used to add logging to a block of code any time a value is assigned, to hook up callbacks between asynchronous code (kind of like async/await in C#...) or to handle when remote sources need to be queried vs operating on query expressions (LINQ?)....

And that's the secret.  The .NET platform actually _supports_ monads already, but they're working hard to hide them from developers because they're *scary*.  The async/await feature actually came from F#, which has had full support for monads for years.  LINQ is a carbon copy of a very well known monad for querying lazy sequences, with all of the syntax renamed to make it very obvious to SQL users.  So why was C# so low on that list?  Unfortunately, that same familiar SQL syntax makes it awkward to code other monads.  You can do it, but the result doesn't look quite right.

11. What's next

So, that was the cool stuff from language design *last* year.  What about this year?

12. Dependent types

So, all of these cool languages in the top right corner haven't solved the problem with Tuples yet.  But they're working in the right direction, researching something called dependent types.  (Warning, bullshit syntax ahead, since you probably don't know Idris yet)

By now, everyone's used to generics.  You can define a generic List type, create two lists of integers, then add their components up item-wise, and.... oh crap, they're different length.  That's a runtime exception.  Which means our type checker fails.

Dependent types add a new idea to generic types; generic parameters can also be values.  Using them, we can redefine our List type and constructor, and lastly our pairwise-sum method.  Now, when we make our lists, we have to specify their length as an integer in our generic arguments, and when we try to add them we get a _compile_ time error.

So that's neat.  What else can they do?  Dependent types can also be used to document and enforce state changes.  Does that method you just call close the socket you sent with it when it's done?  Does it ensure that the background thread it started is still running?  Does it accept any File object, or only files in "Write" or "ReadWrite" mode?  The code examples for these are a bit more complicated to show, so I'm going to gloss over them for now, but there are 3 langauges actively doing research in this area.  Idris and Adga are two langauges researching Dependent Types, and Plaid is a programming language developing what are known as "Typestates", essentially encoding a type state-machine in the type system, allowing it to enforce high level state changes throughout your program.

13. Back to the tuple problem

Okay, so back to the tuple problem.... it's still here!  There's still no good solution to this problem.  Oddly, C++ and typed Lisps come closest by using compile-time templating and macros to create the appropriate classes ahead of time.  This approach works well and keeps compile time safety, but greatly complicates compile times.  So I count it as another escape hatch.

What we'd really like is a fantastical langauge that lets you do things like this.

But we're not there yet.

14. Back to Clojure

So what does Clojure say about all this?  Type systems just aren't worth all the effort.  Sure, you get some free checks out of them, but at best that's a false hope.  The type system simply cannot catch everything at compile time, some things just simply aren't known until runtime, and to test those you need Unit tests.  So forget them completely.  It greatly simplifies your code and lets you focus on the things that matter: the logic, and the tests.

This is exactly the opinion of people like Alan Kay.  Type systems provide some safety, but they're just not worth the effort.

15. So what's the point

Regardless of whether you're a fan of static typing or not, it's clear there's a lot of research and development being done in the area of programming language design.  Liberating yourself of a compromised type systems is a challenge and requires a very different mindset when approaching problems, but can yield surprisingly elegent and flexible solutions.  It's as easy to grind yourself into a rut and forget to look at what new languages have to offer as it is to fall in love with a shiny new language that doesn't really fix anything other than superficial problems.  It's clear, to me at least, that the perfect programming language hasn't been found, and that there is potential room for improvement.

Keep your eye out on these languages - their features have a funny way of sneaking into more popular languages, especially in C#.  When you look at a new language, try to look past syntax changes and shiney chrome to the core principles underneath.  This is what my year and a half long journey to getting into StrangeLoop has been about; learning as much as I can about a very basic component of the tools I use every day; Types.