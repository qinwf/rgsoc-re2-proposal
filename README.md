# GSoC 2016 Proposal - RE2 regular expressions in R

| **Project Info**      |                                         |
|:----------------------|-----------------------------------------|
| **Project Page**      | https://git.io/v26vG                    |
| **R Package Page**    | https://github.com/qinwf/re2r           |

I have been in touch with the mentors on GitHub before submitting this proposal.

## Problem Description

R is a free software environment for statistical computing and graphics. R provides two types of regular expressions in `base` package, extended regular expressions (the default) with TRE and Perl-like regular expressions used by `perl = TRUE` with PCRE. 

PCRE includes useful features, such as named capture, but it uses a backtracking algorithm, so it is easy to take exponential time or arbitrary stack depth for certain regular expressions. Using PCRE in the service backend would have left it open to easy denial of service attacks.

TRE has a polynomial time complexity but does not include named capture.

`stringi` is a R package use the regular expression engine from the ICU library, which has an exponential time complexity. The `stringi` package does not support named capture yet because it is still considered as experimental in ICU. 

RE2 is a primarily DFA based regular expression engine from Google that is fast at matching large amounts of text with named capture. Users can build fast and scalable service backend with RE2 library.

This project will create an R package interface to the RE2 library, providing the R community with the first regular expression package with both named capture and polynomial time complexity.

## Implementation Plan

The project consists of three components:

+ R interface to RE2 library.
+ Proper documentation, tests and benchmarks for the package.
+ Package vignette with introduction, syntax reference, R regular expression package comparison and real-world text data usage examples and popular regular expressions examples like email, www search, etc.

Before submitting this proposal, the student has started building the `re2r` package with basic functionality during the test part of this project.

`re2r` package now provides these functions:

`re2_match()` - match patterns in a character vector, return boolean vector or matched character matrix.

`re2_replace()` - replace matched patterns in a character vector.

`re2_extract()` - extract one matched pattern in a character vector.

`re2()` - create a pre-compiled regular expression.

`%<~%` `%!~%` `%=~%` - binary operator to create a pre-compiled regular expression or check a pattern.

and some other helper functions to get the properties of a pre-compiled regular expression.

Features to be implemented:

1. Implementation in R-C interface and compare it with the Rcpp implementation.
1. Make package cross platform.
1. Unicode and international support.
1. Package unit tests.
1. Package benchmarks.
1. Package documentation and tutorial.
1. CRAN submission.

## Timeline

This week-by-week timeline provides a rough guideline of how the project will be done.

Accepted student proposals announced on 22 April.

**Community Bonding Period**

22 April - 8 May

Familiarize with the RE2 library and the R community.  

9 -- 15 May

Read the source code and document for RE2 library, and Rcpp package, and read *Writing R Extensions* to learn how to build R package. 

16 -- 22 May

Look for examples of how regular expressions are used in existing R packages.

**Work Period**

23 -- 29 May

Write test cases for `re2r` package. Test and document existing code more thoroughly.

30 May -- 5 June

Write extensive benchmarks, covering real-world text data samples and popular regular expressions like email, web search. 

Profile the performance of a `re2r` package.

6 -- 12 June

Try remove `Rcpp` dependency, and compare the lines of code and performance.

13 -- 19 June

Improve unicode and international support.

20 -- 26 June

Write package tutorial and rewrite some existing packages to use `re2r` package to gain user experience of the package.

**Mid-term Evaluations**

27 June -- 10 July

Improve package public function with previous package usage experience. 

11 -- 17 July

Begin submitting mid-term evaluations.

18 -- 31 July

Further refine tests and documentation for the whole project. 

Tests will cover RE2 library unit tests, test cases in `namedCapture` R package, and test cases for unicode and international support. These tests will cover all public functions.

1 -- 7 August

Cross platform test and prepare CRAN submission.

8 -- 14 August

Write the package public release announcement, and publish the first release of the package.

**Final Week**

15 -- 21 August

Begin submitting final evaluations.
