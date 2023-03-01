# Coding Style Guide Meta Document

## 1. Summary

This document describes the process and discussions that led to the Coding
Style PER. Its goal is to explain the reasons behind each decision.

## 2. Why Bother?

PSR-12 was accepted in 2019 and since then a number of changes have been made to PHP,
most notably recent changes for PHP 8 and PHP 8.1, which have implications for coding style
guidelines. Whilst PSR-12 is very comprehensive of PHP functionality that existed at
the time of writing, new functionality is very open to interpretation. PSR-12 seeks
to provide a set way that both coding style tools can implement, projects can declare
adherence to and developers can easily relate on between different projects for these
coding style reducing cognitive friction.

PSR-12 was an update for PSR-2 which was created based upon the common practices of the PHP-FIG
projects at the time but ultimately this meant it was a compromise of many of the different
projects' guidelines. The repercussions of projects changing their coding guidelines to align
with PSR-2 (Almost all projects do align with PSR-1, even if it is not explicitly stated) were
seen to be too great (losing git history, huge changesets and breaking existing patches/pull requests).

PSR-2 required adopters to reformat large amounts of existing code which stifled adoption.
To help alleviate this issue with PSR-12, we have taken a more prescriptive approach and
defined the standards for new language features as they are released.

However, it is for a lack of wanting to be dictatorial that we aimed to apply PSR-2
styling, rationale and stances (Described in Section 4, Approaches) in PSR-12 instead of
establishing new conventions.

The same approach is applied to the current PER.

## 3. Scope

### 3.1. Goals

This PER shares the same goals as PSR-12.

> The intent of this guide is to reduce cognitive friction when scanning code from
> different authors. It does so by enumerating a shared set of rules and expectations
> about how to format PHP code.
> When various authors collaborate across multiple projects, it helps to have one set
> of guidelines to be used among all those projects. Thus, the benefit of this guide is
> not in the rules themselves, but in the sharing of those rules.

This PER extends, expands and replaces PSR-12, and is therefore also an extension of PSR-1.
With PSR-12 being the base of this PER, a list of differences is provided below to assist with migration,
but it should be considered as an independent specification.

This PER will eventually incorporate and replace any stylistic requirements found in PSR-1.
PSR-1 includes a number of non-stylistic requirements that affect runtime behavior, which are
out of scope for this PER. If a particular rule is mentioned in both this PER and PSR-1,
this PER takes precedence. If not, the PSR-1 rule (including errata) still applies.

This PER will include coding style guidelines related to new functionality added to PHP
after the publication of PSR-12, as well as clarifications on the text of PSR-12.
It is a goal of this PER to maintain style consistency between related old and new PHP syntax,
such as class constants and constants in enumerations. In rare cases, this may cause new
releases to include coding style guidelines that break backwards compatibility, limited by
the non-goals and versioning sections below.

### 3.2. Non-Goals

It is not the intention of this PER to substantially or arbitrarily alter coding style guidelines found in PSR-1 and PSR-12.
It will not change anything stipulated in PSR-1 that concerns technical interoperability or runtime behaviour.

## 4. Approaches

The overarching approach is to attempt to apply existing PSR-12 styling and rationale to
new functionality as opposed to establishing new conventions.

### 4.1. Strict Types Declarations

There was a discussion about whether strict types should be enforced in the standard
https://github.com/cs-extended/fig-standards/issues/7. All were in agreement we should only
use a MUST or MUST NOT statement and avoid the use of a SHOULD statement and nobody wanted
to say that strict types could not be declared. The discussion was whether it should be
considered a coding style item which should be covered or whether it was out of scope, and it
was decided to be out of scope of a coding style guide.

### 4.2. Finally and Return Types Declaration Spacing

Numerous options were suggested, and they can be seen
[here for return type declarations](https://gist.github.com/michaelcullum/c025f3870c9ea1dd2668#file-returntypesspacing-php) or
[here for finally blocks](https://gist.github.com/michaelcullum/c025f3870c9ea1dd2668#file-finallyblocks-php)
and the current implementation was chosen due to consistency with other parts of the standard.

### 4.3. Enforcing short form for all type keywords

PHP 7.0 introduced [scalar types declaration](http://php.net/manual/en/functions.arguments.php#functions.arguments.type-declaration)
which does not support long type aliases. Therefore, it makes sense to enforce primary short type forms to be used to
have uniform syntax and prevent possible confusion.

### 4.4. Public Survey

In order to settle things using data, survey was conducted and responses from 142 people
including 17 project representatives were gathered:

#### 4.4.1. PHP-FIG Representative Results

| Representative          | Project           | Compound namespaces with a depth of two or more MUST not be used | Header statement grouping and ordering | Declare statements must each be on their own line | Declare statements in PHP files containing markup | Declare statements have no spaces: `declare(strict_types=1);` | Block declare statement formatting | `new` keyword usage, parenthesis required |Return type declaration formatting |Use statement leading slashes disallowed | Block namespace declaration formatting | General operator spacing |Try, Catch, Finally formatting | Anonymous class declaration formatting | Keyword casing, only lower case | Type keywords, short form only |
| --------------          | -------           | ---------------------------------------------------- | ---------------------------------- | ----------------------------------------- | ------------------------------------------- | -------------------------------------------------------- | ------------------------------- | ------------------------------------- |------------------------------- |------------------------------------ | ----------------------------------- | ---------------------- |--------------------------- | ----------------------------------- | --------------------------- | -------------------------- |
| Alexander Makarov       |  Yii framework    | ✓ | ✓ | ✓ | ❌ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Korvin Szanto           | concrete5         | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Leo Feyer               | Contao            | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Larry Garfield          | Drupal            | ✓ | ✓ | ✓ | ✓ | ✓ | ❌ | ✓ | ✓ | ✓ | ❌ | ✓ | ✓ | ❌ | ✓ | ✓ |
| André R.                | eZ                | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Jan Schneider           | Horde             | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Karsten Dambekalns      | Neos and Flow     | ✓ | ✓ | ✓ | ✓ | ❌ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Andres Gutierrez        | Phalcon           | ❌ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Ryan Thompson           | PyroCMS           | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ❌ | ❌ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Matteo Beccati          | Revive Adserver   | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ❌ | ✓ | ✓ | ✓ | ✓ |
| Damian Mooyman          | SilverStripe      | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Brian Retterer          | Stormpath PHP SDK | ✓ | ✓ | ✓ | ❌ | ❌ | ✓ | ❌ | ✓ | ❌ | ✓ | ✓ | ✓ | ✓ | ❌ | ❌ |
| Matthew Weier O'Phinney | Zend Framework    | ❌ | ✓ | ✓ | ❌ | ✓ | ✓ | ✓ | ❌ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Jordi Boggiano          | Composer          | ❌ | ❌ | ❌ | ✓ | ✓ | ✓ | ❌ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Ben Marks               | Magento           | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Chuck Burgess           | PEAR              | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
|                         | **Totals**:       |13/3|15/1|15/1|13/3|14/2|15/1|14/2|15/1|14/2|14/2|15/1|16/0|15/1|15/1|15/1|

#### 4.4.2. General non-representative voters

| Question | For | Against | Percentage For |
| -------- | --- | ------- | -------------- |
| Compound namespaces required depth | 114 | 12 | 89.47% |
| Header statement grouping and ordering | 113 | 13 | 88.5% |
| Declare statements must each be on their own line | 120 | 6 | 95% |
| Declare statements in PHP files containing markup | 119 | 7 | 94.12% |
| Declare statements have no spaces | 116 | 10 | 91.38% |
| Block declare statement formatting | 118 | 8 | 93.22% |
| `new` keyword usage, parenthesis required | 116 | 10 | 91.38% |
| Return type declaration formatting | 115 | 11 | 90.43% |
| Use statement leading slashes disallowed | 118 | 8 | 93.22% |
| Block namespace declaration formatting | 120 | 6 | 95% |
| General operator spacing | 123 | 3 | 97.56% |
| Try, Catch, Finally formatting | 124 | 2 | 98.39% |
| Anonymous class declaration formatting | 117 | 9 | 92.31% |
| Keyword casing, only lower case | 124 | 2 | 98.39% |
| Type keywords, short form only | 121 | 5 | 95.87% |

### 4.5. Multiline Function Arguments Mixed With Multiline Return

A potential readability issue [was raised on the mailing list](https://groups.google.com/d/msg/php-fig/ULSL4gqK8GY/cgDELuPOCQAJ).
We reviewed options for changes to the specification that could provide better readability and
the floated option was to require a blank line after the opening bracket of a function if the
arguments and the return are both multiline. Instead, it was pointed out that this specification
_already_ allows you to decide where you'd like to add blank lines, and so we will leave it to
the implementors to decide.

## 5. Changelog

Please note this changelog is not a verbose list of changes from PSR-12 and further but highlights the most
notable changes. It should be considered a new specification, and therefore you should read the
specification for a full understanding of its contents.

### 5.1. New Statements

* Lowercase for all keywords - Section 2.5
* Short form for all type keywords - Section 2.5
* Use statement grouping - Section 3
* Use statement blocks - Section 3
* Declare statement/Strict types declaration usage - Section 3
* Parentheses are always required for class instantiation - Section 4
* Typed properties - Section 4.3
* Return type declarations - Section 4.5
* Variadic and reference argument operators - Section 4.5
* Type hints - Section 4.5
* Add finally block - Section 5.6
* Operators - Section 6
* Unary operators - Section 6.1
* Binary operators - Section 6.2
* Ternary operators - Section 6.3
* Anonymous classes - Section 8

### 5.2. Clarifications and Errata

* Adjust 'methods' to 'methods and functions' in a number of instances - Throughout
* Adjust references to classes and interfaces to also include traits - Throughout
* StudlyCaps meaning clarified as PascalCase - Section 2.1
* The last line should not be blank but contain an EOL character - Section 2.2
* Blank lines may be added for readability except where explicitly forbidden within the PSR - Section 2.3
* PSR-2 errata statement about multi-line arguments - Section 4
* PSR-2 errata statement about extending multiple interfaces - Section 4
* Forbid blank lines before/after closing/opening braces for classes - Section 4

## 6. People

### 6.1.  Editor:

* Korvin Szanto

### 6.2. Sponsor:

* Chris Tankersley

### 6.3. Working Group Members:

* Alexander Makarov
* Ken Guest
* Larry Garfield
* Luke Diggins
* Woody Gilk

### 6.4. Special Thanks

* Everyone involved in PSR-1, PSR-2, PSR-12.

## 7. Votes

* **Entrance Vote:** https://groups.google.com/g/php-fig/c/YqPDYGK0RhM/m/pJmThkNKBgAJ

## 8. Relevant Links

_**Note:** Order descending chronologically._

* **PSR-12:** https://www.php-fig.org/psr/psr-12/
* **PSR-2:** https://www.php-fig.org/psr/psr-2/
* **PSR-1:** https://www.php-fig.org/psr/psr-1/
