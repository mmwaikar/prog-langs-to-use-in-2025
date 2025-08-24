# Language Trivia

Let's look at some programming language trivia.

## Language Families

| Family | Languages | Defining Feature |
|--------|-----------|------------------|
| C | Java, C#, JavaScript |
| Lisp | Clojure, [Common Lisp](https://lisp-lang.org/), [Scheme](https://www.scheme.org/) | Macros (code which generates code) |
| ML | [OCaml](https://ocaml.org/), [F#](https://fsharp.org/) | Type Inference |

## Indentation Sensitive Languages

Some programming languages (such as Python, Haskell, and YAML) use indentation to denote nesting, as opposed to special non-whitespace tokens (such as { and } in C++/JavaScript). Even F# uses this style and Scala 3 adopted this style, thereby breaking compatibility with Scala 2.

The significance of this feature is that seemingly fine code may *fail to compile*. e.g. **the below F# code will not compile** -

```fsharp
let x =
if true then 3
else 5
```

The following is the correct code (because of *proper indentation*) -

```fsharp
let x =
    if true then 3
    else 5
```

There are, as usual, both **pros & cons** of this approach.

An advantage is that code written by anyone will **look similar**. So for example, an improperly indented C# code will still compile (but won't so with F#) -

```csharp
if true {
return "hi";    
} else {
            return "hello";
}
```
> **NOTE:** Linters available with the IDEs will probably auto-correct above code and properly indent it, but if you purposefully indent it badly, the code still compiles.

A big disadvantage is that sometimes when you copy-paste code, then you might have to adjust the indentation levels, **so pick your side**.
