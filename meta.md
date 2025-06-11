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
styling, rationale and stances (Described in Section 5, Approaches) in PSR-12 instead of
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

This PER will include coding style guidelines related to new functionality added to PHP
after the publication of PSR-12. This PER will also include clarifications on the text of
PSR-12.

The question of whether to include or replace requirements from PSR-1 was examined by the Working Group. However it was decided to omit any such requirements for further consideration in a subsequent release.

### 3.2. Non-Goals

It is not the intention of this PER to add entirely new coding style guidelines. It will
also not change anything stipulated in PSR-1 and PSR-12.

## 4. Versioning

New releases of this PER are assigned version numbers in keeping with [semantic versioning](https://semver.org/). 
Semantic versioning is well defined when applied to software releases but has no common definition in other contexts. 
This PER applies the following meanings:

* **Patch** versions may contain:
  * Any changes that do not alter the underlying requirements of this PER, such as fixing typos, adding clarifications or 
other modifications with no compatibility impact.
* **Minor** versions may additionally:
  * Add new requirements for PHP syntax previously unspecified in this PER.
  * Add, remove or alter requirements in a way that is both more permissive and backwards compatible for implementers.
* **Major** versions may additionally:
  * Add, remove or alter any requirements.

Projects are expected to pin their own coding style guidelines to a major version of this PER, allowing for regular 
upgrades to minor and patch releases as they are published. When performing such upgrades, it is intended that no change
to existing code is required to maintain compliance with all requirements and recommendations of this PER. This ensures 
new code contributions processed by an automatic formatter follow (or disregard) recommendations consistently with the 
existing code.

Please note this backwards compatibility promise does not extend to projects that use new PHP syntax yet to be specified
in this PER. In this circumstance, a minor version may introduce new requirements that are effectively breaking changes.

It is ultimately determined whether a meaningful change may be included in a minor release on a case-by-case basis by 
consensus. The addition of `MAY` or `OPTIONAL` requirements or the removal of requirements with non-optional RFC 2119 
keywords will not always meet the criteria for minor release. For example, specifying that projects may use tabs instead
of spaces for indentation creates a new implicit requirement that projects must use one style consistently; this new 
burden on projects to reformat incoming contributions to their chosen style defines the change as major.

## 5. People

### 5.1.  Editor:

* Larry Garfield

### 5.2. Sponsor:

* Chris Tankersley

### 5.3. Working Group Members:

* Alexander Makarov
* Ken Guest
* Korvin Szanto
* Luke Diggins

### 7.4. Special Thanks

* Everyone involved in PSR-1, PSR-2, PSR-12.

## 8. Votes

* **Entrance Vote:** https://groups.google.com/g/php-fig/c/YqPDYGK0RhM/m/pJmThkNKBgAJ

## 9. Relevant Links

_**Note:** Order descending chronologically._

* **[Migration Document: PER-CS v2.0 to v3.0](migration-3.0.md)**
* **[Migration Document: PER-CS v1.0 to v2.0](migration-2.0.md)**
* **PSR-12:** https://www.php-fig.org/psr/psr-12/
* **PSR-2:** https://www.php-fig.org/psr/psr-2/
* **PSR-1:** https://www.php-fig.org/psr/psr-1/
