# Migrating from PER-CS v2.0 to PER-CS v3.0 ###

## Summary

PER-CS is the next evolution of the PSR set of Coding Standards from the
PHP-FIG (Framework Interoperability Group). It extends the Coding Standards
laid out in PSR-12 to the newest functionality added to PHP such as the match
keyword, enums, attributes, and more.

This document describes the changes and additions on a section by section
basis between PER-CS v3.0 and PER-CS v2.0.

It is derived in part from [a GitHub-generated diff](https://github.com/php-fig/per-coding-style/compare/2.0.0...3.0.0#files_bucket)
and focuses on the changes on a section-by-section basis as its focus is to be more readable.

This document intends to provide a summary of these changes that can
then be used to drive action lists for toolset producers to support PER-CS v3.0.

This document is non-normative.  The published [3.0 PER-CS](https://www.php-fig.org/per/coding-style/) specification 
is the canonical source for the PER-CS formatting expectations.

## [Section 2.5 - Keywords and Types](https://www.php-fig.org/per/coding-style/#25-keywords-and-types)

Formatting conventions are now provided for compound types (those that include union or intersection type declarations).

* The `|` and `&` symbols and parentheses MUST NOT have leading or trailing spaces.
* If a type declaration is long enough to split to multiple lines, each ANDed block must be on one line, and each ORed block on its own line.
* If one of the types listed is `null`, it must come last.
* Favor `?` over `|null` in cases where both work.
* A multi-catch statement must follow the same rules.  (See section 5.6 as well.)

```php
function foo(int|string $a): User|Product
{
    // ...
}

function complex(array|(ArrayAccess&Traversable) $input): ArrayAccess&Traversable
{
    // ...
}

function veryComplex(
    array
    |(ArrayAccess&Traversable)
    |(Traversable&Countable) $input): ArrayAccess&Traversable
{
    // ...
}
```

## [Section 2.7 - Naming](https://www.php-fig.org/per/coding-style/#27-naming)

PER-CS now recommends following the same naming conventions as PHP Internals for abbreviations and acronyms.  Specifically, only uppercase the first character of the acronym: `XmlFormatter`, not `XMLFormatter`.

## [Section 3 - Declare Statements, Namespace, and Import Statements](https://www.php-fig.org/per/coding-style/#3-declare-statements-namespace-and-import-statements)

The `<?php` tag must always be all-lowercase.

## [Section 4 - Classes, Properties, and Methods](https://www.php-fig.org/per/coding-style/#4-classes-properties-and-methods)

If using PHP 8.4 or later, parentheses should be omitted around a `new` declaration.

## [Section 4.3 - Properties and Constants](https://www.php-fig.org/per/coding-style/#43-properties-and-constants)

Class constants must have a visibility and type declared.

If a property has a `set`-visibility defined, the `get` visibility may be omitted.

```php
class Foo
{
    // This is allowed.
    private(set) string $name;
}
```

## [Section 4.6 - Modifier Keywords](https://www.php-fig.org/per/coding-style/#46-modifier-keywords)

At least one of `readonly`, `get`-visibility, and `set`-visibility must be specified.  If at least one is specified, the others may be omitted.

```php
class Foo
{
    // These are all acceptable.
    public private(set) string $one;
    private(set) string $two;
    readonly string $three;

    // These are not.
    private(set) public string $four;
}
```

## [Section 4.7 - Methods and Function Calls](https://www.php-fig.org/per/coding-style/#47-method-and-function-calls)

The `exit()` and `die()` functions should always be called with parentheses, even though PHP technically permits them without.

## [Section 4.9 - Property hooks](https://www.php-fig.org/per/coding-style/#49-property-hooks)

Formatting guidelines for property hooks are now included.

When using property hooks on a constructor promoted property, only single-line set hooks are allowed.  Anything more complicated MUST be defined separately from the constructor.

The following are examples of properly formatted hooks:

```php
class Example
{
    public string $one = 'Me' {
        set(string $value) {
            // ...
        }
    }

    public string $two {
        get {
            // ...
        }
        set {
            // ...
        }
    }
    
    public string $three {
        get => __CLASS__;
        set => ucfirst($value);
    }
    
    public string $four { get => __CLASS__; }
}
```

## [Section 5.2 - Switch, Case, and Match](https://www.php-fig.org/per/coding-style/#52-switch-case-match)

When breaking a series of boolean operators across multiple lines, the operator MUST be at the beginning of each line, not the end of each line.

(This applies to `switch`, `match`, `while`, `do while`, and any other expression.)

## [Section 6.4 - Operator placement](https://www.php-fig.org/per/coding-style/#64-operator-placement)

When breaking a series of chained operations across multiple lines, the operator MUST be at the beginning of each line, not the end of each line, and all lines but the first MUST be indented.  Examples include `??` and ternary conditionals.

```php
<?php

$variable1 = $ternaryOperatorExpr
    ? 'fizz'
    : 'buzz';

$variable2 = $possibleNullableExpr
    ?? 'fallback';

$variable3 = $elvisExpr
    ?: 'qix';
```
