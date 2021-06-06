---
layout: splash
classes: wide
title: 'Book Notes: Programming Interviews Exposed'
excerpt: 'Book notes &mdash; Programming interviews exposed : secrets to landing your next job / John Mongan, Eric Giguère, Noah Kindler.'
date: 2021-06-06
permalink: /posts/2021/05/programming-interview-exposed/
tags:
  - interview
  - book review
---

# Programming interviews exposed : secrets to landing your next job / John Mongan, Eric Giguère, Noah Kindler.

## Big-*O* Analysis in Action
``` c
CompareToMax(array, n) {
    for i, i < n, i++ {
        if array[i] > curMax {
            curMax = array[i]
        }
    }
}
```
``` c
CompareToAll(array, n) {
    for i = n-1, i > 0, i-- {
        for j = 0, j < n, j++ {
            if array[j] > array[i] {
                isMax = false /* not the largest value in the array
                break
            }
        }
    }
}
```
- input size *n*
- as *n* approaches infinity, the difference between *n* and *n* + *2* is insignificant, so the constant term can be ignored
- the difference between *n<sup>2</sup>* and *n* + *n<sup>2</sup>* is negligible for a very large *n*
- **eliminate all but the highest-order term**

### Best, Average and Worst Cases
`CompareToAll`

Worst | Average | Best
----- | ------- | ----
max value at end of array | max value in middle, check only half *n* times | max value at beginning of array
O(*n<sup>2</sup>*) | *n*(*n*/2) = *n<sup>2</sup>*/2 times, O(*n<sup>2</sup>*/2)<br/>actual time dependent on machine, 1/2 doesn't mean much, so stil(*n<sup>2</sup>*) | O(*n*)

### How to Do Big-*O* Analysia
1. Figure out what the input is and what *n* represents.
1. Express the number of operations the algorithm performs in terms of *n*.
1. Eliminate all but the highest-order terms.
1. Remove all  constant factors.

### Which Algorithm is Better?
O(1) &mdash; fastest-possible running time, *constant running time*, ideal but rarely achievable

| | | *n* = 10 | double *n* = 20
---|---|---|---
*logarithmic* &mdash; increases logarihtmically to input size | O(log *n*) | log 10 = 1 | log 20 = 1.30
*linear algorithm* &mdash; direct propostion to input size | O(*n*) | 10 = 10 | 20 = 20
*superlinear algorithm* &mdash; between linear and polynomial | O(*n* log *n*) | 10 log 10 = 10 | 20 log 20 = 26.02
*polynomial algorithm* &mdash; grows quickly based on input size | O(*n<sup>c</sup>*) | 10<sup>2</sup> = 100 | 20<sup>2</sup> = 400
*exponential algorithm* &mdash; grows even faster | O(*c<sup>n</sup>*) | 2<sup>10</sup> = 1024 | 2<sup>20</sup> = 1048576
*factorial algorithm* &mdash; grows the fastest | O(*n!*) | 10! = 3628800 | 20! = 2.43x10<sup>18</sup>

constant, logarithmic , linear or superlinear time are preferred