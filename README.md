## Minimallist

A minimalist data driven data model library, inspired by [Clojure Spec](https://clojure.org/guides/spec) and [Malli](https://github.com/metosin/malli).

## Features

- no macro, no static registry, pure functions.
- fully data driven, models are hash-map based,
- support recursive definitions, sequence regex,
- relatively simple implementation, very short to read (about 100 lines of code)
- helpers functions to create the hash-map models painlessly,
- cross platform (`.cljc`)

## Non-features

- does not integrate with anything else,
- does not try hard to be performant,
- no roadmap or timeline: I made this library mainly for my own usage, and I take my time.

## Usage

```clojure
(ns your-namespace
  (:require [minimallist.core :refer [valid?]]
            [minimallist.helper :as h]))

(def hiccup-model
  (h/let ['hiccup (h/alt [:node (h/in-vector (h/cat (h/fn keyword?)
                                                    (h/? (h/map))
                                                    (h/* (h/not-inlined (h/ref 'hiccup)))))]
                         [:primitive (h/or (h/fn nil?)
                                           (h/fn boolean?)
                                           (h/fn number?)
                                           (h/fn string?))])]
    (h/ref 'hiccup)))

(valid? hiccup-model [:div {:class [:foo :bar]}
                      [:p "Hello, world of data"]])
```

See the [tests](test/) for more examples of how to use the helpers to build your models.

## Status

This is a work in progress, the API may change in the future.

More functionalities will be added later, once the API design is more stable.

If you find any bug or have comments, please create an issue in GitHub.

## License

The Minimallist library is developed by Vincent Cantin.
It is distributed under the terms of the Eclipse Public License version 2.0.
