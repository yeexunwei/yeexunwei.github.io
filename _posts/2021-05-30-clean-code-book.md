---
title: 'Clean Code book notes'
date: 2021-05-30
permalink: /posts/2012/08/blog-post-1/
tags:
  - clean code
  - book review
---

# Clean code : a handbook of agile software craftsmanship / Robert C. Martin

## 2 Meaningful Names

- Use intention-revealing names
    - ```
        int d; elapsed time in days
        ```
        `d` reveals nothing
        ```
        int elapsedTimeInDays;
        ```
- Avoid disinformation
- Make meaningful distinctions
    - `a1, a2, ..., aN` is noninformative
    - `ProductInfo` or `ProductData` are indistince noise words
    - ```
        getActiveAccount();
        getActiveAccounts();
        getActiveAccountInfo();
        ```
- Use pronounceable names
- **Use searchable names**
    - single-letter names and numeric constants are difficult to locate
    - single-letter names can ONLY be used as local variables insided short methods
- Avoid encodings
    - Member prefixes `_m`
    - Interfaces and implementations `ShapeFactoryImp` > `CShapeFactroy` > `IShapeFactory`
        - `I` is distraction at best and too much information at worst
- Avoid mental mapping
    - readers shouldn't have to mentally translate names into other names they already know
    - `i` or `j` or `k` (though never `l`) for loop counters are traditional (fine)
- Class names
    - should have noun or noun phrases
- Method names
    - should have verb or verb phrases
    - accessors, mutators and predicates should be named for their value and prefixed with `get`, `set` and `is` (javabean standard)
- Don't be cute
- Pick one word per concept
    - confusing to have `fetch`, `retrieve` and `get`
    - `controller`, `manager` and `driver`
- Don't pun
    - avoid using the same word for two purposes
- Use solution domain names
    - readers are programmers
    - use CS terms, algorithms names, pattern names, math terms and so forth
- Use problem domain names
- Add meaningful context

