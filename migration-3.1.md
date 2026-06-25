# Migrating from PER-CS v3.0 to PER-CS v3.1 ###

## Summary

PER-CS is the next evolution of the PSR set of Coding Standards from the
PHP-FIG (Framework Interoperability Group). It extends the Coding Standards
laid out in PSR-12 to the newest functionality added to PHP such as the match
keyword, enums, attributes, and more.

This document describes the changes and additions on a section by section
basis between PER-CS v3.1 and PER-CS v3.0.

It is derived in part from [a GitHub-generated diff](https://github.com/php-fig/per-coding-style/compare/3.0.0...3.1.0#files_bucket)
and focuses on the changes on a section-by-section basis as its focus is to be more readable.

This document intends to provide a summary of these changes that can
then be used to drive action lists for toolset producers to support PER-CS v3.1.

This document is non-normative. The published [3.1 PER-CS](https://github.com/php-fig/per-coding-style/blob/3.1.0/spec.md) specification 
is the canonical source for the PER-CS formatting expectations.

## [Section 4.7 - Method and Function Calls](https://github.com/php-fig/per-coding-style/blob/3.1.0/spec.md#47-method-and-function-calls)

The `clone()` function SHOULD always be called with parenthesis, even when the optional `$withProperties` argument is not provided. For example:

```php
<?php

$b = clone($a);
$b = clone($a, [
    'foo' => 'bar',
]);
```

## [Section 5.2 - Switch, Case, and Match](https://github.com/php-fig/per-coding-style/blob/3.1.0/spec.md#52-switch-case-match)

The formatting rules for `switch` and `case` have been expanded and clarified:

* A `case` body MUST NOT be wrapped in `{}`.
* Every non-empty `case` MUST end with a terminating statement (`break`, `return`, or similar), even if it is the last one in the `switch` block.
* If a `case` condition is complex enough to warrant being multi-line, it MUST be wrapped in parentheses, with the opening parenthesis on the same line as the `case` keyword and a final line containing only the closing parenthesis and colon.

```php
<?php

switch (true) {
    case (
        $a === 10
        && $b === 20
    ):
        doSomething();
        break;
}
```

## [Section 6.2 - Binary operators](https://github.com/php-fig/per-coding-style/blob/3.1.0/spec.md#62-binary-operators)

The pipe operator `|>` is now listed among the binary operators and, like the others, MUST be preceded and followed by at least one space.

```php
<?php

$result = $input |> trim(...) |> strtoupper(...);
```

## [Section 6.4 - Operator placement](https://github.com/php-fig/per-coding-style/blob/3.1.0/spec.md#64-operators-placement)

When a chain of pipe operators is split across multiple lines, the `|>` operator MUST be at the beginning of each line, and all lines but the first MUST be indented, following the same rule as other chained operators.

```php
<?php

$result = '<foo>'
    |> strtoupper(...)
    |> htmlspecialchars(...);
```

## [Section 7 - Closures](https://github.com/php-fig/per-coding-style/blob/3.1.0/spec.md#7-closures)

If a closure contains no statements, then the body MUST be abbreviated as `{}` and placed on the same line as the previous symbol, separated by a space. If possible, empty-body closures SHOULD be replaced with arrow functions.

```php
<?php

$noOpFunction = function () {};

// SHOULD be preferred where possible:
$noOpFunction = fn() => null;
```

## [Section 8 - Anonymous Classes](https://github.com/php-fig/per-coding-style/blob/3.1.0/spec.md#8-anonymous-classes)

Formatting guidelines for attributes on anonymous classes are now included. If an anonymous class has attributes, they MUST be placed starting on the next line after the `new` keyword, indented once, and otherwise follow the same rules as other attributes specified in section 12. The remaining anonymous class declaration after the final attribute MUST start on a new line and keep the same indentation as the attributes:

```php
<?php

$example = new
    #[Attribute]
    class {
        // ...
    };
```

## [Section 9 - Enumerations](https://github.com/php-fig/per-coding-style/blob/3.1.0/spec.md#9-enumerations)

Non-public enum methods were already required to use `private` instead of `protected`, as enums do not support inheritance. This rule was extended to also apply to constants.

```php
<?php

enum Size
{
    case Small;
    case Medium;
    case Large;

    private const Huge = self::Large;
}
```
