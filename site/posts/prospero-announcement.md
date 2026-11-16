---
title: "Announcing Prospero: a strongly-typed configuration language with Haskell-like syntax"
author: Phil Curzon
date: Nov 16, 2026
tags: [Prospero, Functional programming, Infrastructure as Code, Configuration]
description: Announcing my new configuration language Prospero which has Haskell-like syntax and evaluates to JSON or YAML.

---

I'm announcing [Prospero](https://codeberg.org/theinnerlight/prospero) - a new configuration language with Haskell-like syntax that currently evaluates to JSON or YAML.

For a good few years now, I've been investigating the space of configuration languages like Dhall and Nickel. If you have to write complex configuration when working with the likes of terraform or kubernetes, these kinds of languages can drastically reduce the amount of complexity you're confronted with and the volume of repetitive code you have to maintain. Despite their perfect fit for the problem space, I've never been entirely happy with any of the language options already available: I've been hungry for more type system features and the powerful type inference that languages like Haskell have treated us to.

Late last year, I completed a major infrastructure as code project in Pulumi. It offers another arguably compelling solution to a similar problem: generate configuration in a mainstream programming language. I've encountered similar ideas from time to time: Scala's `sbt` is another one I've used a fair bit that does something similar, letting you write your project's build configuration in Scala.

These kinds of approaches are extremely powerful but they come at a tremendous cost in both the amount and the types of complexity you have to deal with in configuration. In my opinion, being able to write arbitrary side effects and arbitrary non-terminating code in configuration isn't a feature, it's a category error.

So, I decided to try and build a language that meets all of my needs more precisely.

Prospero has a type system that features:

- Powerful type inference
- Parametric (including higher-kinded) polymorphism
- Structural record types
- Algebraic data types (ADTs) + pattern matching
- Type classes (including multi-parameter type classes)
- Unit of measure
- Rank-N types
- Pure functions only (no side effects allowed)
- Only structural recursion (without manual church-encoding)

Here is a little taster:

`example.ppo`
```haskell
measure MiB
measure GiB = <1024 MiB>

data Service = Service
  { name : String
  , memory : Integer<MiB>
  , replicas : Int
  }

memoryFootprint : [Service] -> Integer<MiB>
memoryFootprint s = sum <| map (\x -> x.memory * x.replicas) s

let services =
  [ Service
      { name = "api"
      , memory = 512<MiB>
      , replicas = 3
      }
  , Service
      { name = "postgres"
      , memory = 2<GiB>
      , replicas = 1
      }
  ]

toString <| memoryFootprint services
```

Running `prospero evaluate --to-json example.ppo` prints:

```
"3584 MiB"
```

#### Structural recursion

```haskell
data Nat
  = Zero
  | Succ Nat

toInt : Nat -> Int
toInt n = case n of
  Zero   -> 0
  Succ m -> 1 + toInt m

toInt (Succ (Succ (Succ (Succ Zero))))
```

Prospero accepts the above and it evaluates to 4.

If you instead wrote (using `n` instead of `m`)...

```haskell
toInt : Nat -> Int
toInt n = case n of
  Zero   -> 0
  Succ m -> 1 + toInt n
```

...you would see ``elaboration error: `toInt` is recursive, but no argument gets structurally smaller on every recursive call``

----

Prospero is currently an early prototype. I'm sharing it mostly to find out if people are interested and what features I should spend time on next. If you're looking for a mature and production-proven configuration language, I recommend Dhall.

At this stage, please do not expect:

- A language server
- Error messages with useful source metadata (outside of the parser)
- Any kind of polished user experience

On the other hand, you might see:

- Parser bugs
- Compiler bugs/crashes
- Breaking changes in language syntax*
- Termination checker escapes
- Weird performance characteristics

Here are some things I'm thinking about adding in the future:

- Source annotations + language server
- Dhall-style semantic hashing
- Remote (URL) imports
- More compilation targets, e.g. TOML, Nix, etc.
- Expanded prelude with more built-in type classes
- Idiom brackets (syntactic sugar over Applicative)

Thoughts, ideas and contributions are all very much welcome.

**[Try Prospero](https://codeberg.org/theinnerlight/prospero)**
