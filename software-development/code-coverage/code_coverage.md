---
title: "Code Coverage"
tags:
  - Software Development Life Cycle
  - code coverage
---

# What is Code Coverage?

Code Coverage is a measure that describes the degree to which code has been tested.

## How it works?

One of the possibilities is to implement checks throughout the code, run the test utile, and then analysing how many of those checks were actually running.

## How is Code Coverage calculated?

The four main metrics used are:
- __statement coverage__: how many of the statements in the program have been executed.
- __branch coverage__: how many of the branches of each control structures have been executed.
- __condition coverage__: for each boolean sub-expression, were they tested for both true and false?
- __function/subroutine coverage__: how many of the declared functions have been called during testing?

Other metrics:
- __decision coverage__: a combination of function coverage and branch coverage.
- __multiple condition coverage__: where all combinations of conditions inside each decision have to be tested.
- __linear code sequence and jump coverage__
- __path coverage__
- __entry/coverage__
- __loop coverage and stage coverage__
- __Parameter value coverage__: all common values for each parameter should be tested.
- ...

## Why Code Coverage matters?

Good indicator if your code base is well tested. However, you shouldn't follow the 100% coverage goal since it doesn't necesserally mean that your code is well tested.
