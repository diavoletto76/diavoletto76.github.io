---
title:  "Element promotion"
categories: programming
tags: clojure challenge
---
Clojure weekly challenge by Eric Normand.

## Problem

Sometimes you have a list and you want to "promote" one element toward the front of the list. Essentially, you need to swap the element with its immediate predecessor (if it exists). Write a function promote that takes a predicate and a list. If the predicate is true, the element should be promoted.

## Examples

```clojure
(promote even? [1 3 5 6]) ;=> (1 3 6 5)
(promote even? []) ;=> ()
(promote even? [2 1]) ;=> (2 1)
(promote even? [0 2 4 6]) ;=> (0 2 4 6)
(promote even? [0 1 2 3 4 5 6]) ;=> (0 2 1 4 3 6 5)
(promote even? [1 2 2 2 2]) ;=> (2 2 2 2 1)
```

## Solutions

It took me some time to dicide how to handle the case of two consecitive items, for both of which the predicate (`even?` our the example) returns `true`: items should not be swaped!

```clojure
(defn promote [f xs]
  (loop [[x1 x2 & xs] xs acc []]
    (cond (nil? x1) acc
          (nil? x2) (conj acc x1)
          (and (f x2) ((complement f) x1)) (recur (cons x1 xs) (conj acc x2))
          :else (recur (cons x2 xs) (conj acc x1)))))
```

## Resources

- [Eric Normand/Element promotion](https://gist.github.com/ericnormand/098143e8cdbecef0faeba92f730b9cba)
