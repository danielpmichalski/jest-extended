<div align="center">
  <h1>jest-extended</h1>

  🃏💪

  Additional Jest matchers
</div>

<hr />

[![Build Status](https://img.shields.io/travis/jest-community/jest-extended.svg?style=flat-square)](https://travis-ci.org/jest-community/jest-extended)
[![Code Coverage](https://img.shields.io/codecov/c/github/jest-community/jest-extended.svg?style=flat-square)](https://codecov.io/github/jest-community/jest-extended)
[![version](https://img.shields.io/npm/v/jest-extended.svg?style=flat-square)](https://www.npmjs.com/package/jest-extended)
[![downloads](https://img.shields.io/npm/dm/jest-extended.svg?style=flat-square)](http://npm-stat.com/charts.html?package=jest-extended&from=2017-09-14)
[![MIT License](https://img.shields.io/npm/l/jest-extended.svg?style=flat-square)](https://github.com/jest-community/jest-extended/blob/master/LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com)
[![Roadmap](https://img.shields.io/badge/%F0%9F%93%94-roadmap-CD9523.svg?style=flat-square)](https://github.com/jest-community/jest-extended/blob/master/docs/ROADMAP.md)
[![Examples](https://img.shields.io/badge/%F0%9F%92%A1-examples-ff615b.svg?style=flat-square)](https://github.com/jest-community/jest-extended/blob/master/docs/EXAMPLES.md)

## Problem

Jest is an amazing test runner and has some awesome assertion APIs built in by default. However there are times when
having more specific matchers (assertions) would be far more convenient.

## Solution

jest-extended aims to add additional matchers to Jest's default ones making it easy to test everything 🙌

## Contributing

If you've come here to help contribute - Thanks! Take a look at the [contributing](/CONTRIBUTING.md) docs as a way of getting started.

---

- [Problem](#problem)
- [Solution](#solution)
- [Contributing](#contributing)
- [Installation](#installation)
- [Setup](#setup)
- [API](#api)
    - [.pass(message)](#passmessage)
    - [.fail(message)](#failmessage)
    - [.toBeEmpty()](#tobeempty)
    - [.toBeOneOf([members])](#tobeoneofmembers)
    - [.toBeNil()](#tobenil)
    - [.toSatisfy(predicate)](#tosatisfypredicate)
  - [Array](#array)
    - [.toBeArray()](#tobearray)
    - [.toBeArrayOfSize()](#tobearrayofsize)
    - [.toIncludeAllMembers([members])](#toincludeallmembersmembers)
    - [.toIncludeAnyMembers([members])](#toincludeanymembersmembers)
    - [.toIncludeSameMembers([members])](#toincludesamemembersmembers)
    - [.toSatisfyAll(predicate)](#tosatisfyallpredicate)
  - [Boolean](#boolean)
    - [.toBeBoolean()](#tobeboolean)
    - [.toBeTrue()](#tobetrue)
    - [.toBeFalse()](#tobefalse)
  - [Date](#date)
    - [.toBeDate()](#tobedate)
    - [.toBeValidDate()](#tobevaliddate)
    - [.toBeAfter(date)](#tobeafterdate)
    - [.toBeBefore(date)](#tobebeforedate)
    - Further proposals in [#117](https://github.com/jest-community/jest-extended/issues/117) PRs welcome
  - [Function](#function)
    - [.toBeFunction()](#tobefunction)
  - [Mock](#mock)
    - [.toHaveBeenCalledBefore()](#tohavebeencalledbefore)
    - [.toHaveBeenCalledAfter()](#tohavebeencalledafter)
  - [Number](#number)
    - [.toBeNumber()](#tobenumber)
    - [.toBeNaN()](#tobenan)
    - [.toBeFinite()](#tobefinite)
    - [.toBePositive()](#tobepositive)
    - [.toBeNegative()](#tobenegative)
    - [.toBeEven()](#tobeeven)
    - [.toBeOdd()](#tobeodd)
    - [.toBeWithin(start, end)](#tobewithinstart--end)
  - [Object](#object)
    - [.toBeObject()](#tobeobject)
    - [.toContainKey(key)](#tocontainkeykey)
    - [.toContainKeys([keys])](#tocontainkeyskeys)
    - [.toContainAllKeys([keys])](#tocontainallkeyskeys)
    - [.toContainAnyKeys([keys])](#tocontainanykeyskeys)
    - [.toContainValue(value)](#tocontainvaluevalue)
    - [.toContainValues([values])](#tocontainvaluesvalues)
    - [.toContainAllValues([values])](#tocontainallvaluesvalues)
    - [.toContainAnyValues([values])](#tocontainanyvaluesvalues)
    - [.toContainEntry([key, value])](#tocontainentrykey--value)
    - [.toContainEntries([[key, value]])](#tocontainentrieskey--value)
    - [.toContainAllEntries([[key, value]])](#tocontainallentrieskey--value)
    - [.toContainAnyEntries([[key, value]])](#tocontainanyentrieskey--value)
    - [.toBeExtensible()](#tobeextensible)
    - [.toBeFrozen()](#tobefrozen)
    - [.toBeSealed()](#tobesealed)
  - [~~Promise~~](#promise)
  - [String](#string)
    - [.toBeString()](#tobestring)
    - [.toBeHexadecimal(string)](#tobehexadecimal)
    - [.toEqualCaseInsensitive(string)](#toequalcaseinsensitivestring)
    - [.toStartWith(prefix)](#tostartwithprefix)
    - [.toEndWith(suffix)](#toendwithsuffix)
    - [.toInclude(substring)](#toincludesubstring)
    - [.toIncludeRepeated(substring, times)](#toincluderepeatedsubstring--times)
    - [.toIncludeMultiple([substring])](#toincludemultiplesubstring)
- [Contributors](#contributors)
- [LICENSE](#license)

## Installation

With npm:
```sh
npm install --save-dev jest-extended
```

With yarn:
```sh
yarn add -D jest-extended
```

## Setup

Add jest-extended to your Jest setupTestFrameworkScriptFile configuration. [See for help](http://facebook.github.io/jest/docs/en/configuration.html#setuptestframeworkscriptfile-string)

``` json
"jest": {
  "setupTestFrameworkScriptFile": "jest-extended"
}
```

If you are already using another test framework, like [jest-chain](https://github.com/mattphillips/jest-chain), then you should create a test setup file and `require` each of the frameworks you are using.

For example:

```js
// ./testSetup.js
require('jest-extended');
require('any other test framework libraries you are using');
```

Then in your Jest config:

```json
"jest": {
  "setupTestFrameworkScriptFile": "./testSetup.js"
}
```

## API

#### .pass(message)

_Note: Currently unimplemented_

Passing assertion.

```js
expect().pass('should pass');
```

#### .fail(message)

_Note: Currently unimplemented_

Failing assertion.

```js
expect().fail('test should fail');
```

{{sandbox/matchers/toBeEmpty.test.js}}

{{sandbox/matchers/toBeOneOf.test.js}}

{{sandbox/matchers/toBeNil.test.js}}

{{sandbox/matchers/toSatisfy.test.js}}

### Array

{{sandbox/matchers/array/toBeArray.test.js}}

{{sandbox/matchers/array/toBeArrayOfSize.test.js}}

{{sandbox/matchers/array/toIncludeAllMembers.test.js}}

{{sandbox/matchers/array/toIncludeAnyMembers.test.js}}

{{sandbox/matchers/array/toIncludeSameMembers.test.js}}

{{sandbox/matchers/array/toSatisfyAll.test.js}}

### Boolean

{{sandbox/matchers/boolean/toBeBoolean.test.js}}

{{sandbox/matchers/boolean/toBeTrue.test.js}}

{{sandbox/matchers/boolean/toBeFalse.test.js}}

### ~~Date~~

Proposal in #117 (*under development*)

{{sandbox/matchers/date/toBeDate.test.js}}

{{sandbox/matchers/date/toBeValidDate.test.js}}

{{sandbox/matchers/date/toBeAfter.test.js}}

{{sandbox/matchers/date/toBeBefore.test.js}}

### Function

{{sandbox/matchers/function/toBeFunction.test.js}}

### Mock

{{sandbox/matchers/mock/toHaveBeenCalledBefore.test.js}}

{{sandbox/matchers/mock/toHaveBeenCalledAfter.test.js}}

### Number

{{sandbox/matchers/number/toBeNumber.test.js}}

{{sandbox/matchers/number/toBeNaN.test.js}}

{{sandbox/matchers/number/toBeFinite.test.js}}

{{sandbox/matchers/number/toBePositive.test.js}}

{{sandbox/matchers/number/toBeNegative.test.js}}

{{sandbox/matchers/number/toBeEven.test.js}}

{{sandbox/matchers/number/toBeOdd.test.js}}

{{sandbox/matchers/number/toBeWithin.test.js}}

### Object

{{sandbox/matchers/object/toBeObject.test.js}}

{{sandbox/matchers/object/toContainKey.test.js}}

{{sandbox/matchers/object/toContainKeys.test.js}}

{{sandbox/matchers/object/toContainAllKeys.test.js}}

{{sandbox/matchers/object/toContainAnyKeys.test.js}}

{{sandbox/matchers/object/toContainValue.test.js}}

{{sandbox/matchers/object/toContainValues.test.js}}

{{sandbox/matchers/object/toContainAllValues.test.js}}

{{sandbox/matchers/object/toContainAnyValues.test.js}}

{{sandbox/matchers/object/toContainEntry.test.js}}

{{sandbox/matchers/object/toContainEntries.test.js}}

{{sandbox/matchers/object/toContainAllEntries.test.js}}

{{sandbox/matchers/object/toContainAnyEntries.test.js}}

{{sandbox/matchers/object/toBeExtensible.test.js}}

{{sandbox/matchers/object/toBeFrozen.test.js}}

{{sandbox/matchers/object/toBeSealed.test.js}}

### ~~Promise~~

_No APIs proposed yet_

### String

{{sandbox/matchers/string/toBeString.test.js}}

{{sandbox/matchers/string/toBeHexadecimal.test.js}}

{{sandbox/matchers/string/toEqualCaseInsensitive.test.js}}

{{sandbox/matchers/string/toStartWith.test.js}}

{{sandbox/matchers/string/toEndWith.test.js}}

{{sandbox/matchers/string/toInclude.test.js}}

{{sandbox/matchers/string/toIncludeRepeated.test.js}}

{{sandbox/matchers/string/toIncludeMultiple.test.js}}

## Contributors

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
| [<img src="https://avatars0.githubusercontent.com/u/5610087?v=4" width="100px;"/><br /><sub>Matt Phillips</sub>](http://mattphillips.io)<br />[📝](#blog-mattphillips "Blogposts") [💻](https://github.com/mattphillips/jest-extended/commits?author=mattphillips "Code") [📖](https://github.com/mattphillips/jest-extended/commits?author=mattphillips "Documentation") [💡](#example-mattphillips "Examples") [🚇](#infra-mattphillips "Infrastructure (Hosting, Build-Tools, etc)") [⚠️](https://github.com/mattphillips/jest-extended/commits?author=mattphillips "Tests") | [<img src="https://avatars1.githubusercontent.com/u/611927?v=4" width="100px;"/><br /><sub>Stephen Bluck</sub>](https://github.com/stevebluck)<br />[💻](https://github.com/mattphillips/jest-extended/commits?author=stevebluck "Code") [⚠️](https://github.com/mattphillips/jest-extended/commits?author=stevebluck "Tests") | [<img src="https://avatars3.githubusercontent.com/u/5880416?v=4" width="100px;"/><br /><sub>Christoffer Hasselberg</sub>](https://github.com/stofolus)<br />[💻](https://github.com/mattphillips/jest-extended/commits?author=stofolus "Code") | [<img src="https://avatars1.githubusercontent.com/u/20847518?v=4" width="100px;"/><br /><sub>Brandon Newton</sub>](https://btnwtn.com)<br />[💻](https://github.com/mattphillips/jest-extended/commits?author=btnwtn "Code") [📖](https://github.com/mattphillips/jest-extended/commits?author=btnwtn "Documentation") [⚠️](https://github.com/mattphillips/jest-extended/commits?author=btnwtn "Tests") | [<img src="https://avatars2.githubusercontent.com/u/4533277?v=4" width="100px;"/><br /><sub>Devan Patel</sub>](http://www.devanpatel.me)<br />[💻](https://github.com/mattphillips/jest-extended/commits?author=devanp92 "Code") [📖](https://github.com/mattphillips/jest-extended/commits?author=devanp92 "Documentation") | [<img src="https://avatars2.githubusercontent.com/u/8472688?v=4" width="100px;"/><br /><sub>Gary Leutheuser</sub>](https://GaryLeutheuser.github.io)<br />[💻](https://github.com/mattphillips/jest-extended/commits?author=GaryLeutheuser "Code") | [<img src="https://avatars3.githubusercontent.com/u/24882614?v=4" width="100px;"/><br /><sub>Johan Lindgren</sub>](https://github.com/lindgr3n)<br />[💻](https://github.com/mattphillips/jest-extended/commits?author=lindgr3n "Code") [📖](https://github.com/mattphillips/jest-extended/commits?author=lindgr3n "Documentation") [⚠️](https://github.com/mattphillips/jest-extended/commits?author=lindgr3n "Tests") |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| [<img src="https://avatars1.githubusercontent.com/u/159848?v=4" width="100px;"/><br /><sub>Andrew Hayward</sub>](http://andrewhayward.net)<br />[💻](https://github.com/mattphillips/jest-extended/commits?author=andrewhayward "Code") [⚠️](https://github.com/mattphillips/jest-extended/commits?author=andrewhayward "Tests") | [<img src="https://avatars3.githubusercontent.com/u/6209178?v=4" width="100px;"/><br /><sub>Oliver Schneider</sub>](https://ols.io)<br />[💻](https://github.com/mattphillips/jest-extended/commits?author=olsio "Code") [⚠️](https://github.com/mattphillips/jest-extended/commits?author=olsio "Tests") | [<img src="https://avatars1.githubusercontent.com/u/22359375?s=460&v=4" width="100px;"/><br /><sub>Tyle Whalen</sub>](https://github.com/tjwhalen16)<br />[💻](https://github.com/mattphillips/jest-extended/commits?author=tjwhalen16 "Code") [📖](https://github.com/mattphillips/jest-extended/commits?author=tjwhalen16 "Documentation") | [<img src="https://avatars2.githubusercontent.com/u/17944339?v=4" width="100px;"/><br /><sub>Martius</sub>](https://github.com/martiuslim)<br />[💻](https://github.com/mattphillips/jest-extended/commits?author=martiuslim "Code") [⚠️](https://github.com/mattphillips/jest-extended/commits?author=martiuslim "Tests") | [<img src="https://avatars2.githubusercontent.com/u/10856932?v=4" width="100px;"/><br /><sub>Eli Collis</sub>](https://github.com/ecollis6)<br />[💻](https://github.com/mattphillips/jest-extended/commits?author=ecollis6 "Code") | [<img src="https://avatars0.githubusercontent.com/u/10706203?v=4" width="100px;"/><br /><sub>Marcin Lichwała</sub>](https://github.com/marcinlichwala)<br />[💻](https://github.com/mattphillips/jest-extended/commits?author=marcinlichwala "Code") [⚠️](https://github.com/mattphillips/jest-extended/commits?author=marcinlichwala "Tests") | [<img src="https://avatars3.githubusercontent.com/u/1984733?v=4" width="100px;"/><br /><sub>Massimo Prencipe</sub>](https://github.com/mprencipe)<br />[💻](https://github.com/mattphillips/jest-extended/commits?author=mprencipe "Code") [⚠️](https://github.com/mattphillips/jest-extended/commits?author=mprencipe "Tests") |
| [<img src="https://avatars2.githubusercontent.com/u/33098064?v=4" width="100px;"/><br /><sub>mjmiles</sub>](https://github.com/mjmiles)<br />[💻](https://github.com/mattphillips/jest-extended/commits?author=mjmiles "Code") [📖](https://github.com/mattphillips/jest-extended/commits?author=mjmiles "Documentation") | [<img src="https://avatars1.githubusercontent.com/u/13333582?v=4" width="100px;"/><br /><sub>Gary Meehan</sub>](https://github.com/garmeeh)<br />[💻](https://github.com/mattphillips/jest-extended/commits?author=garmeeh "Code") [📖](https://github.com/mattphillips/jest-extended/commits?author=garmeeh "Documentation") [⚠️](https://github.com/mattphillips/jest-extended/commits?author=garmeeh "Tests") | [<img src="https://avatars2.githubusercontent.com/u/3191489?v=4" width="100px;"/><br /><sub>Fredrik Mäkilä</sub>](https://github.com/GitHug)<br />[💻](https://github.com/mattphillips/jest-extended/commits?author=GitHug "Code") [⚠️](https://github.com/mattphillips/jest-extended/commits?author=GitHug "Tests") | [<img src="https://avatars2.githubusercontent.com/u/9046616?v=4" width="100px;"/><br /><sub>Daniel Reinoso</sub>](http://kloc.io/)<br />[💻](https://github.com/mattphillips/jest-extended/commits?author=danielr18 "Code") [⚠️](https://github.com/mattphillips/jest-extended/commits?author=danielr18 "Tests") | [<img src="https://avatars1.githubusercontent.com/u/4359781?v=4" width="100px;"/><br /><sub>Chris Hut</sub>](https://github.com/tophernuts)<br />[💻](https://github.com/mattphillips/jest-extended/commits?author=tophernuts "Code") [⚠️](https://github.com/mattphillips/jest-extended/commits?author=tophernuts "Tests") | [<img src="https://avatars2.githubusercontent.com/u/1513183?v=4" width="100px;"/><br /><sub>Kelvin Ly</sub>](https://github.com/cactorium)<br />[💻](https://github.com/mattphillips/jest-extended/commits?author=cactorium "Code") [⚠️](https://github.com/mattphillips/jest-extended/commits?author=cactorium "Tests") | [<img src="https://avatars0.githubusercontent.com/u/11182826?v=4" width="100px;"/><br /><sub>Francis Ngo</sub>](https://github.com/francisngo)<br />[💻](https://github.com/mattphillips/jest-extended/commits?author=francisngo "Code") [⚠️](https://github.com/mattphillips/jest-extended/commits?author=francisngo "Tests") |
| [<img src="https://avatars1.githubusercontent.com/u/10330923?v=4" width="100px;"/><br /><sub>Amish Shah</sub>](https://hydrabolt.me/)<br />[💻](https://github.com/mattphillips/jest-extended/commits?author=hydrabolt "Code") [⚠️](https://github.com/mattphillips/jest-extended/commits?author=hydrabolt "Tests") | [<img src="https://avatars3.githubusercontent.com/u/2045206?v=4" width="100px;"/><br /><sub>Dave Cooper</sub>](http://davecooper.org)<br />[💻](https://github.com/mattphillips/jest-extended/commits?author=grug "Code") [⚠️](https://github.com/mattphillips/jest-extended/commits?author=grug "Tests") | [<img src="https://avatars3.githubusercontent.com/u/3630495?v=4" width="100px;"/><br /><sub>Swann Polydor</sub>](https://github.com/soueuls)<br />[💻](https://github.com/mattphillips/jest-extended/commits?author=soueuls "Code") [⚠️](https://github.com/mattphillips/jest-extended/commits?author=soueuls "Tests") | [<img src="https://avatars1.githubusercontent.com/u/2027003?v=4" width="100px;"/><br /><sub>vikneshwar</sub>](https://github.com/vikneshwar)<br />[💻](https://github.com/mattphillips/jest-extended/commits?author=vikneshwar "Code") [⚠️](https://github.com/mattphillips/jest-extended/commits?author=vikneshwar "Tests") | [<img src="https://avatars1.githubusercontent.com/u/1243921?v=4" width="100px;"/><br /><sub>Budi Irawan</sub>](http://budiirawan.com)<br />[💻](https://github.com/mattphillips/jest-extended/commits?author=deerawan "Code") [⚠️](https://github.com/mattphillips/jest-extended/commits?author=deerawan "Tests") | [<img src="https://avatars2.githubusercontent.com/u/980783?v=4" width="100px;"/><br /><sub>Tejas Bubane</sub>](http://foss-geek.blogspot.com/)<br />[💻](https://github.com/mattphillips/jest-extended/commits?author=tejasbubane "Code") [⚠️](https://github.com/mattphillips/jest-extended/commits?author=tejasbubane "Tests") [📖](https://github.com/mattphillips/jest-extended/commits?author=tejasbubane "Documentation") | [<img src="https://avatars2.githubusercontent.com/u/13134653?v=4" width="100px;"/><br /><sub>Subinoy Ghosh</sub>](https://github.com/subinoy7)<br />[💻](https://github.com/mattphillips/jest-extended/commits?author=subinoy7 "Code") [⚠️](https://github.com/mattphillips/jest-extended/commits?author=subinoy7 "Tests") |
| [<img src="https://avatars1.githubusercontent.com/u/1404810?v=4" width="100px;"/><br /><sub>Simen Bekkhus</sub>](https://github.com/SimenB)<br />[📖](https://github.com/mattphillips/jest-extended/commits?author=SimenB "Documentation") | [<img src="https://avatars2.githubusercontent.com/u/49038?v=4" width="100px;"/><br /><sub>Orta</sub>](http://orta.io)<br />[📖](https://github.com/mattphillips/jest-extended/commits?author=orta "Documentation") | [<img src="https://avatars3.githubusercontent.com/u/17221813?v=4" width="100px;"/><br /><sub>Tom</sub>](https://jsdevtom.com)<br />[💻](https://github.com/mattphillips/jest-extended/commits?author=jsdevtom "Code") [📖](https://github.com/mattphillips/jest-extended/commits?author=jsdevtom "Documentation") [💡](#example-jsdevtom "Examples") [⚠️](https://github.com/mattphillips/jest-extended/commits?author=jsdevtom "Tests") | [<img src="https://avatars0.githubusercontent.com/u/15064535?v=4" width="100px;"/><br /><sub>Lucian Buzzo</sub>](https://github.com/LucianBuzzo)<br /> | [<img src="https://avatars3.githubusercontent.com/u/2997844?v=4" width="100px;"/><br /><sub>Thiago Delgado Pinto</sub>](https://github.com/thiagodp)<br />[💻](https://github.com/mattphillips/jest-extended/commits?author=thiagodp "Code") [📖](https://github.com/mattphillips/jest-extended/commits?author=thiagodp "Documentation") [💡](#example-thiagodp "Examples") [🤔](#ideas-thiagodp "Ideas, Planning, & Feedback") [⚠️](https://github.com/mattphillips/jest-extended/commits?author=thiagodp "Tests") | [<img src="https://avatars0.githubusercontent.com/u/3042904?v=4" width="100px;"/><br /><sub>Ragnar Laud</sub>](https://github.com/xprn)<br />[💻](https://github.com/mattphillips/jest-extended/commits?author=xprn "Code") [📖](https://github.com/mattphillips/jest-extended/commits?author=xprn "Documentation") | [<img src="https://avatars0.githubusercontent.com/u/3047126?v=4" width="100px;"/><br /><sub>Luiz Américo</sub>](https://github.com/blikblum)<br />[💻](https://github.com/mattphillips/jest-extended/commits?author=blikblum "Code") |
| [<img src="https://avatars0.githubusercontent.com/u/615334?v=4" width="100px;"/><br /><sub>Frederick Fogerty</sub>](https://github.com/frederickfogerty)<br />[💻](https://github.com/mattphillips/jest-extended/commits?author=frederickfogerty "Code") [🤔](#ideas-frederickfogerty "Ideas, Planning, & Feedback") | [<img src="https://avatars1.githubusercontent.com/u/10714808?v=4" width="100px;"/><br /><sub>Benjamin Kay</sub>](https://github.com/benjaminkay93)<br />[💻](https://github.com/mattphillips/jest-extended/commits?author=benjaminkay93 "Code") [📖](https://github.com/mattphillips/jest-extended/commits?author=benjaminkay93 "Documentation") | [<img src="https://avatars1.githubusercontent.com/u/868844?v=4" width="100px;"/><br /><sub>Gilles De Mey</sub>](https://demey.io)<br />[💻](https://github.com/mattphillips/jest-extended/commits?author=gillesdemey "Code") [📖](https://github.com/mattphillips/jest-extended/commits?author=gillesdemey "Documentation") [⚠️](https://github.com/mattphillips/jest-extended/commits?author=gillesdemey "Tests") | [<img src="https://avatars0.githubusercontent.com/u/50928?v=4" width="100px;"/><br /><sub>Deniz Dogan</sub>](https://github.com/denizdogan)<br />[💻](https://github.com/mattphillips/jest-extended/commits?author=denizdogan "Code") | [<img src="https://avatars1.githubusercontent.com/u/13043635?v=4" width="100px;"/><br /><sub>Mikey Powers</sub>](https://github.com/mvpowers)<br />[💻](https://github.com/mattphillips/jest-extended/commits?author=mvpowers "Code") [📖](https://github.com/mattphillips/jest-extended/commits?author=mvpowers "Documentation") [⚠️](https://github.com/mattphillips/jest-extended/commits?author=mvpowers "Tests") |
<!-- ALL-CONTRIBUTORS-LIST:END -->

## LICENSE

[MIT](/LICENSE)