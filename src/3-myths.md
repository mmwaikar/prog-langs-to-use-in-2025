# Myths

Let's start with a few myths. I am calling them myths because programmers who are familiar with only one family of languages, tend to think that this is the only way, but it is not so.

- **Myth 1** - Dashes `-` are not allowed in function names.
- **Fact** - Not true. Although, most languages do not allow this and follow different conventions, e.g. JVM languages follow `camelCase`, .Net languages follow `PascalCase`, Rust follows `snake_case` (my least favorite, I think it makes the language look more system-y 😉), however, Clojure follows `kebab-case` so it allows dashes in the function / variable names. This is the convention I like most, as it is the most readable (for my tastes, at least) e.g. `calculateInterest` vs. `calculate-interest`.

---
**Fun fact**: how many keystrokes needed for each convention?

| Word | Convention | # Keystrokes |
|------|------------|--------------|
| helloWorld | camelCase | 11 [10 (chars) + 1 (Shift key for upper-case)] |
| HelloWorld | PascalCase | 12 [10 (chars) + 2 (Shift keys for upper-case)]] |
| hello_world | snake_case | 12 [10 (chars) + 2 (Shift + - for underscore)] |
| hello-world | kebab-case | 11 [10 (chars) + 1 (- key for dash)] |
---

- **Myth 2** - Question marks `?` are not allowed in function names.
- **Fact** - Not true. Predicates are functions which return a boolean, e.g. `isEven` or `isPrime`. Since most languages do not allow `?` you have to follow some conventions like prefixing `is` to the predicate function name, but again I like Clojure's convention the best. So, in Clojure, predicate functions end with a `?` - so `isEven` would be named `even?` and `isPrime` would be named `prime?`. **Can't be more clearer, right?**

- **Myth 3** - Every statement has to end with a `;`
- **Fact** - Not true. F#, Scala, Python don't need a trailing `;` to end a statement. In fact, programmers who love Lisp family of languages, call it the **cancer of semicolons** 😉 whereas, people who hate Lisp (or Lisp family of languages) describe Lisp as **Lots of Irritating Superfluous Parentheses**

- **Myth 4** - You use a `return` keyword to return a value from a function
- **Fact** - Not true.

Look at this F# function -

```fsharp
let add a b =
    a + b
```

Curiously, Rust takes a **mixed approach**. The difference is *so subtle* that you may miss it until you actually start writing code (at least, it happened with me). Rust uses `;` to end a statement but you can omit both the `return` keyword AND the `;` to return a value from a function -

```rust
fn add(a: i32, b: i32) -> i32 {
    // first statement ends with a ;
    let sum = a + b;

    // to return a value, don't use the return keyword AND don't end with a ;
    sum
}
```

The above style is **the idiomatic way** but it can also be written as -

```rust
fn add(a: i32, b: i32) -> i32 {
    let sum = a + b;
    return sum;
}
```

- **Myth 5** - In typed languages, you have to specify the type of the return value.
- **Fact** - Not true. The Scala compiler is able to infer the return type of the function based on the value of the last expression. So if the programmer fails to mention the return type, the compiler correctly infers so.

```scala
def greet(name: string) {
    s"Hello, $name"
}
```

- **Myth 6** - In typed languages, you have to specify the type of every function parameter.
- **Fact** - This is the **most significant** myth busted by languages that support `type-inference` like the ML family of languages (F#, OCaml) or Haskell. **Type Inference** means that the compiler will try to guess the type of everything (variables, return type of any function or even the types of every function parameter) 😮 e.g. the above F# `add` function - the compiler guesses the type of the function parameters as `int` and so the type of the return value is also `int` (this is represented as `int -> int -> int` meaning the function takes 2 `int` parameters and returns an `int`). *And if you are thinking that this is just a toy example, and it may not work in large code-bases, then you are wrong. The compiler is smart enough to scan all your dependencies and infer correct types. When it is not able to do so, of course, no one is stopping you from specifying the types.* **What this feature enables is reduced development time (the most popular argument given in favour of dynamic languages) while getting extreme type safety, at the same time.**

- **Myth 7** - Function parameters are always specified as a tuple.
- **Fact** - Not true. While most languages follow this e.g. the `add` function in Rust accepts the parameters as a tuple `(a: i32, b: i32)`, let's see how an F# function looks like, if I have to add, say two `doubles` -

```fsharp
let addD a (b: double) =
    a + b
```

Or, to add two `strings` -

```fsharp
let add (a: string) b =
    a + b
```

In the first function, the type of the parameter `a` and the return type is obviously inferred as `double` while the second function, the type of the parameter `b` and the return type is obviously inferred as `string`. **A very interesting outcome of this way of specifying each parameter with its type, separately, is that all the functions are implicitly** [curried](https://en.wikipedia.org/wiki/Currying). Currying means that if you specify lesser number of arguments than what the function expects (let's say `n`), and if you call the function with `1` argument, then you get another function with `n - 1` parameters. So, if I do this -

```fsharp
let add5 a b = add 5
```

> **NOTE**: Our `add` function expected `2 (n)` parameters, but we called it with only `1` argument, so we get back another function with `2 - 1` (= 1) parameter. So in the above case, `add5` function only expects 1 argument and it will always add 5 to the argument passed to it.

- **Myth 8** - A language compiles to just one target, so Java compiles to JVM bytecode or C# compiles to .Net IL.
- **Fact** - Not true. The modern, functional first (or mixed FP) languages like F#, Scala, Clojure have all *upped the game* by getting compiled to at leat *one more target* (apart from the core target) which has the biggest **reach** of all, *and that target is JavaScript*. And the biggest **game-changer** of all is [Web Assembly](https://webassembly.org/), which enables code compiled to the Wasm format to run in browsers.

So let's see the targets supported by different languages -

| Language | Primary target | JS | Native (C++) | Rust | Python | Dart | PHP | Wasm |
|----------|----------------|----|--------------|------|--------|------|-----|------|
| Clojure | JVM | ClojureScript | [jank](https://jank-lang.org/) | | | [ClojureDart](https://github.com/Tensegritics/ClojureDart) | [Phel](https://phel-lang.org/) | |
| Scala | JVM | [Scala.js](https://www.scala-js.org/) | [Scala Native](https://scala-native.org/en/stable/) | | | | | |
| F# | .Net | [F# Fable](https://fable.io/) | | Fable | Fable | Fable | Fable | [Bolero](https://fsbolero.io/) |
| Rust | Most OSes | | | | | | | [Rust Wasm](https://github.com/rustwasm) |
| C# | .Net | | | | | | | [Blazor](https://dotnet.microsoft.com/en-us/apps/aspnet/web-apps/blazor) |

> **NOTE** Some of the targets supported by Fable e.g. are beta or alpha whereas some are stable. Same goes for targets of other languages.

**But the point to take away is that the more targets a language supports, the more bang you'll get for your buck.**

So in the remaining parts of this series, we'll start discussing about some of the languages that I've worked on and will argue about their pros and cons, so stay tuned.
