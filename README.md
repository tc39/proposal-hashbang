# Hashbang Grammar

This proposal is to match de-facto usage in some CLI JS hosts that allow for [Shebangs / Hashbang](https://en.wikipedia.org/wiki/Shebang_(Unix)). Such hosts strip the hashbang in order to generate valid JS source texts before passing to JS engines currently. This would move the stripping to engines, it does unify and standardize how that is done.

## Example

```mjs
#!/usr/bin/env node
// in the Script Goal
'use strict';
console.log(1);
```

```mjs
#!/usr/bin/env node
// in the Module Goal
export {};
console.log(1);
```

## Status

* Stage: 3
* [Tests](https://github.com/tc39/test262/pull/1983)
* Spec PR: TODO
* Implementations shipping:
  * Chrome Canary 74
  * Firefox Nightly 67

## Why Hashbang instead of Shebang

Hash is commonly associated with modern terms involving `#` such as hashtag. In addition for discoverability, the term "hash sign" is used for `#` but "she sign" is not.

## Why only at the start of a Source Text

Hashbang directives are only valid at the start of a file for interpretters in various CLI environments. There is no gain for the intended usage by allowing it in other places and in fact could lead to confusion since it would not be picked up by CLI environments. Additionally by allowing Hashbang in other places it overlaps a grammar space for `#!` if it is an inifix binary expression of some kind. Use `//` if you want line comments elsewhere.

## Existing Notes from Meetings

* [March 2018](https://tc39.github.io/tc39-notes/2018-03_mar-21.html#10iic-hashbang-grammar-for-stage-2)
* [November 2017](https://tc39.github.io/tc39-notes/2017-11_nov-28.html#10if-interpreterdirective)
