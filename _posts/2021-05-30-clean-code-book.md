---
layout: splash
classes: wide
title: 'Book Notes: Clean Code'
excerpt: 'Book notes &mdash; Clean code : a handbook of agile software craftsmanship / Robert C. Martin'
date: 2021-05-30
published: false
permalink: /posts/2021/05/clean-code/
tags:
  - clean code
  - book review
---

# Clean code : a handbook of agile software craftsmanship / Robert C. Martin

## Chapter 2 Meaningful Names
1. Use intention-revealing names
    - `int elapsedTimeInDays;` > `int d; elapsed time in days`
1. Avoid disinformation
1. Make meaningful distinctions
    - `a1, a2, ..., aN` is noninformative
    - `ProductInfo` or `ProductData` are indistince noise words
    - ```
        getActiveAccount();
        getActiveAccounts();
        getActiveAccountInfo();
        ```
1. Use pronounceable names
1. **Use searchable names**
    - single-letter names and numeric constants are difficult to locate
    - single-letter names can ONLY be used as local variables insided short methods
1. Avoid encodings
    - Member prefixes `_m`
    - Interfaces and implementations `ShapeFactoryImp` > `CShapeFactroy` > `IShapeFactory`
        - `I` is distraction at best and too much information at worst
1. Avoid mental mapping
    - readers shouldn't have to mentally translate names into other names they already know
    - `i` or `j` or `k` (though never `l`) for loop counters are traditional (fine)
1. Class names
    - should have noun or noun phrases
1. Method names
    - should have verb or verb phrases
    - accessors, mutators and predicates should be named for their value and prefixed with `get`, `set` and `is` (javabean standard)
1. Don't be cute
1. Pick one word per concept
    - confusing to have `fetch`, `retrieve` and `get`
    - `controller`, `manager` and `driver`
1. Don't pun
    - avoid using the same word for two purposes
1. Use solution domain names
    - readers are programmers, use CS terms, algorithms names, pattern names, math terms and so forth
1. Use problem domain names
1. Add meaningful context
    - class named `Address` > prefixes: `addrFirstName`, `addrLastName`, `addrState`, ... > `firstName`, `lastName`, `street`, `houseNumber`, `city`, `state` and `zipcode`
1. Don't add gratuitous context
    - shorter names are generally better than longer ones
    - add no more context to name than is necessary

## Chapter 3 Functions
1. Small!
    - two, three or four lines long
    - Blocks and indenting
        - blocks within `if` statements, `else` statements, `while` statements and so on should be one line long (probably function call)
1. Do one thing
    > Functions should do one thing. They should do it well. They should do it only.
    - if function does only those steps that are one level below stated name of function, then function is only doing one thing
    - cannot extract another function from function
    - Sections within functions
        - functions that do one thing  cannot be reasonably divided into sections
1. One level of abstraction per function
    - Reading code from top to bottom: the stepdown rule
1. Switch statements
    - `switch` statements do *N* things
    - bury in low-level class and never repeat - with *polymorphism*
1. Use descriptive names
1. Function arguments
    - 0 > 1 > 2, avoid 3
    - Common monadic forms &mdash; return value is better than output argument
    - Flag arguments &mdash; passing boolean into function is terrible, split function into two
    - Dyadic functions &mdash; try to convert to monads
    - Triads
    - Argument objects &mdash; wrap arguments into class if > 2, 3
    - Argument lists &mdash; if variable arguments are treated identically -> single argument of type `List` `void monad(Object... args);`
    - Verbs and keywords
1. Have no side effects
1. Output arguments
    - `report.appendFooter()` > `public void appendFooter(StringBuffer report)`
1. Command query separation
1. Prefer exceptions to returning error codes
1. Extract try/catch blocks &mdash; extract bodies of `try`  and `catch` blocks out into functions of their own
1. Error handling is one thing
1. Don't repeat yourself
1. Structured programming

## Chapter 4 Comments
1. Comments do not make up for bad code
1. Explain yourself in code
1. Good comments
    - Legal comments &mdash; refer to only standard license
    - Informative comments
    - Explanation of intent
    - Clarification
    - Warning of consequences
    - TODO comments &mdash;`//TODO`
    - Amplification &mdash; `//this is important ...`
1. Bad comments
    - Mumbling
    - Redundant comments
    - Misleading comments
    - Mandated comments
    - Journal comments
    - Noise comments &mdash; restate the obvious and provide no new information
    - Scary noise &mdash; error in comments (copied and pasted)
    - Don't use a comment when you can use a function or a variable
    - Position markers
    - Closing brace comments
    - Attributions and bylines
    - **Commented-out code**
    - HTML comments
    - Nonlocal information
    - Too much information
    - Inobvious connection
    - Function headers

## Chapter 5 Formatting
1. Vertical formatting