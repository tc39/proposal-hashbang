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
  * [Chrome 74](https://www.chromestatus.com/features#milestone%3D74)
  * [Firefox 67](https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/67)
  * [ChakraCore](https://github.com/microsoft/ChakraCore/pull/6145)
  * Node.js 12.0.0

## Why Hashbang instead of Shebang

Hash is commonly associated with modern terms involving `#` such as hashtag. In addition for discoverability, the term "hash sign" is used for `#` but "she sign" is not.

## Why only at the start of a Source Text

Hashbang comments are only valid at the start of a file for interpretters in various CLI environments. There is no gain for the intended usage by allowing it in other places and in fact could lead to confusion since it would not be picked up by CLI environments. Additionally by allowing Hashbang in other places it overlaps a grammar space for `#!` if it is an inifix binary expression of some kind. Use `//` if you want line comments elsewhere.

# Does the hashbang syntax work within `eval` / `Function`?

Hashbang comments are only avilable at the start of a [`Script`](https://tc39.es/ecma262/#prod-Script) or [`Module`](https://tc39.es/ecma262/#prod-Module) parsing goal. Since `eval` uses `Script` it does support Hashbang comments. Since `Function` uses [`FunctionBody`](https://tc39.es/ecma262/#prod-FunctionBody), it does not.

## Interaction with byte-order mark

A [byte-order mark](https://en.wikipedia.org/wiki/Byte_order_mark) (BOM) character at the beginning of a source text will prevent a subsequent `#!` from being interpreted as a hashbang. However, web browsers strip this character as part of fetching external [scripts](https://html.spec.whatwg.org/multipage/webappapis.html#fetch-a-classic-script) or [modules](https://html.spec.whatwg.org/multipage/webappapis.html#fetch-a-single-module-script) (in [`decode`](https://encoding.spec.whatwg.org/#decode) or [`UTF-8 decode`](https://encoding.spec.whatwg.org/#utf-8-decode) respectively), which happens before the text is interpreted as ECMAScript. As such, in browsers a BOM character can precede a `#!` in an external script or module, but not an inline one.

Generally speaking, the BOM character is assumed to be handled by the host, and is not given special treatment by this proposal.

## Existing Notes from Meetings

* [March 2018](https://tc39.github.io/tc39-notes/2018-03_mar-21.html#10iic-hashbang-grammar-for-stage-2)
* [November 2017](https://tc39.github.io/tc39-notes/2017-11_nov-28.html#10if-interpreterdirective)
