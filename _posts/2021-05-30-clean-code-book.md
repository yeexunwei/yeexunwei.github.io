---
layout: splash
classes: wide
title: 'Clean Code book notes'
date: 2021-05-30
permalink: /posts/2021/05/clean-code/
toc: true
tags:
  - clean code
  - book review
---

# Clean code : a handbook of agile software craftsmanship / Robert C. Martin

## Chapter 2 Meaningful Names
1. Use intention-revealing names
    - ```
        int d; elapsed time in days
        ```
        `d` reveals nothing
        ```
        int elapsedTimeInDays;
        ```
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
    - readers are programmers
    - use CS terms, algorithms names, pattern names, math terms and so forth
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
