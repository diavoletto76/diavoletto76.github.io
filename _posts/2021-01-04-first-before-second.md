---
title:  "First before second"
categories: programming
tags: clojure challenge
---
Clojure weekly challenge by Eric Normand.

## Problem

Write a function that takes a string and two letters. The function should return true if every instance of the first letter comes before every instance of the second letter.

Notes:

- Letters will be mixed case. You should treat \A the same as \a.
- You can assume the strings will contain instances of both letters.

## Examples

```clojure
(first-before? "A rabbit jumps joyfully" \a \j) ;=> true
(first-before? "A jolly rabbit jumps joyfully" \a \j) ;=> false
(first-before? "Don't tread on me" \t \m) ;=> true
(first-before? "Every React podcast" \t \d) ;=> false
```

## Solutions

This is the simplest solution I can think of. I'm not sure if it's considered fare, in fact using `last-index-of` and `index-of` the problem becomes somewhat trivial.

```clojure
(defn first-before? [xs a b]
  (< (clojure.string/last-index-of xs a) (clojure.string/index-of xs b)))
```

So I came out with a different solutions which is less elegant, nonetheless it's pretty because it makes use of *recursion* and *lazy evaluation*.

```clojure
(defn indexes-of
  ([xs x] (indexes-of xs x 0))
  ([xs x start]
   (let [i (clojure.string/index-of xs x start)]
     (if (some? i)
       (lazy-seq (cons i (indexes-of xs x (inc i))))
       nil))))

(defn first-before? [xs a b]
   (< (last (indexes-of xs a)) (first (indexes-of xs b))))
```

## Resources

- [Eric Normand/First before second](https://gist.github.com/ericnormand/18a6858ea77c0a306bc75e4b3d7c5ce6)
- [Edabit](https://edabit.com/challenge/D6XfxhRobdQvbKX4v)
