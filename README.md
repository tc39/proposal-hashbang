# Hashbang Grammar

This proposal is to match de-facto usage in some CLI JS hosts that allow for [Shebangs / Hashbang](https://en.wikipedia.org/wiki/Shebang_(Unix)). Such hosts strip the hashbang in order to generate valid JS source texts before passing to JS engines currently. This would unify and standardize how that is done.

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

## Why Hashbang instead of Shebang

Hash is commonly associated with modern terms involving `#` such as hashtag. In addition for discoverability, the term "hash sign" is used for `#` but "she sign" is not.

## Why only at the start of a Source Text

Hashbang directives are only valid at the start of a file for interpretters in various CLI environments. There is no gain for allowing it in other places, and it overlaps a grammar space for `#!` if it is an inifix binary expression of some kind. Use `//` if you want line comments elsewhere.

