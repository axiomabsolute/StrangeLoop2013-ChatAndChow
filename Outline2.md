# StrangeLoop 2013

So, what is StrangeLoop?  StrangeLoop is a technical conference for the geekiest of programming geeks. 

<!-- Super nerdy guy -->

 It's home to people who write new programming languages and optimizing compilers for fun.  It's a place where people perk up for terms like "hygenic macro" and "self verifying compiler". 

<!-- I actually counted seeing this shirt on 7 different people -->
<!-- On the first day alone -->

There was a lot of social awkwardness and starwars tshirts. 

<!-- real programmers use butterflies comic -->

 It's a place full of memes and nerdy internet jokes. It's a crowd where it's borderline _shameful_ to use an IDE.  Vim, Emacs, or GTFO.  I saw exactly one person using a windows machine there.  They were being made fun of.

<!-- popular projects -->

But it's also a gathering of some of the most popular and influential names in the open source community.  These are people who are working on the making "the next java", people who are redefining our industry by releasing amazing products, redefining what it means to program.  StrangeLoop is the birthplace for ideas that get talked about two years from now.

So why'd I go?

<!-- Jokes on me -->

I saw this joke on the internet, and I didn't get it.  I mean, I get the joke, this is an absurd pile of math and computer science I (and I would wager nobody on this room) would get.  But that's it.  I get the joke, but I don't get the material.

So how'd I find this joke, and why did my not understanding it bother me?  Because I asked a few questions, and I found answers more or less along those lines.

This is actually a description of a type inferencing system, actually the one behind F#.  So when you write something crazy

<!-- code block -->
```
let rec factorian n =
  if n  = 0
  then 1
  else n * factorial ( n - 1)
// val vactorial : n:int -> int
```

the F# compiler actually tells you what type things are.  You don't have to write type signatures on almost anything at all.

<!-- add to previous -->
```
let addumUp x y = 
    factorial(x) + factorial(y)
```

It'll figure out most types from usage alone.

```
let makeList a b =
    [a; b]
// val makeList : a:'a -> b:'a -> 'a list
// In C#: List<A> makeList(A firstItem, A secondItem)
```

Even generics.

<!-- So why'd I go? -->

So back to why I went; this is where people talk about problems like these, among other things.  I spent about a year reading up on the kinds of things they talk about at strange loop.  I read about JIT compilers, functional programming, and new models for distributed computing.  But what interested me most were the new languages that were being developed, and the type systems they were based on.  Very closely related to that joke from earlier (which I still don't entirely get, btw).  So most of the talks I attended were based around that topic.  So what'd I learn?

<!-- NPE -->

How many times have people run into null pointer exceptions?  In Java, C#, and C++, even the best programmers are likely to run into them sometimes.  They're annoyingly common enough that we've even built it into our IDEs and other tools to check for them and tell us not to use them.  Did you know there are entire languages where NPEs just don't happen?  C# got close to making it happen, but they backed out before going all the way, with Nullable types.