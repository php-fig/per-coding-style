# Migrating from PER-CS v1.0 (PSR-12) to PER-CS v2.0 ###

## Summary

PER-CS is the next evolution of the PSR set of Coding Standards from the
PHP-FIG (Framework Interoperability Group). It extends the Coding Standards
laid out in PSR-12 to the newest functionality added to PHP such as the match
keyword, enums, attributes, and more.

This document describes the changes and additions on a section by section
basis between PER-CS v2.0 and PER-CS v1.0 (which is a direct equivalent of 
PSR12 with very minor changes).

It is derived in part from [a GitHub generated changelog](https://github.com/php-fig/per-coding-style/compare/1.0.0...2.0.0)
and focuses on the changes in a section-by-section basis as it's focus is to be more readable.

The intent of this document is to provide a summary of these changes that can
then be used to drive action-lists for toolset producers to support PER-CS v2.0.

This document is non-normative.  The published [2.0 PER-CS](https://www.php-fig.org/per/coding-style/) specification 
is the canonical source for the PER-CS formatting expectations.

## [Section 2.6 - Trailing Commas](https://www.php-fig.org/per/coding-style/#26-trailing-commas)

Numerous constructs now allow a sequence of values to have an optional trailing
comma:
 * If the final item is on the same line then there MUST NOT be a trailing comma
 * If the final item is not on the same line then there MUST be a trailing comma

## [Section 4.4 - Methods and Functions](https://www.php-fig.org/per/coding-style/#44-methods-and-functions)

If a function or method contains no statements or comments (such as an empty
no-op implementation or when using constructor property promotion), then the
body SHOULD be abbreviated as {} and placed on the same line as the previous
symbol, separated by a space.
So, for a method of a subclass that does nothing:

    <?php
    class SubClass extends BaseClass
    {
        protected function init() {}
    }

## [Section 4.6 - Modifier Keywords](https://www.php-fig.org/per/coding-style/#46-modifier-keywords)

Modifier keywords are keywords that alter how PHP handles classes,
properties and methods.

These keywords MUST BE ordered as follows:

[abstract|final] [public|protected|private] [static] [readonly]
[type] name

Furthermore all keywords must be on a single line and MUST be separated
by a single space.

## [Section 4.7 - Method and Function Calls](https://www.php-fig.org/per/coding-style/#47-method-and-function-calls)

If using named arguments, there MUST NOT be a space between the argument name and colon, 
and there MUST be a single space between the colon and the argument value.

Method chaining MAY be put on separate lines, where each subsequent line is indented once. When doing so, the first method MUST be on the next line.

## [Section 4.8 - Function Callable References](https://www.php-fig.org/per/coding-style/#48-function-callable-references)

Function callable references - there must not be whitespace surrounding the '...' operator ()

## [Section 5.2 - Switch, Case, Match](https://www.php-fig.org/per/coding-style/#52-switch-case-match)

The match keyword is now covered.

## [Section 7.1 - Short Closures](https://www.php-fig.org/per/coding-style/#71-short-closures)

A new subsection about Short Closures.

As with standard closures, 'fn' must not be succeeded by a space.
The '=>' symbol MUST be preceeded and succeeded by a space. (No leading or trailing spaces)
The semicolon at the end MUST NOT be preceeded by a leading space.
The expression portion MAY be split to a subsequent line. If so, the => MUST be 
included on the second line, and MUST be indented once.

## [Section 9 - Enumerations](https://www.php-fig.org/per/coding-style/#9-enumerations)

Enums are now covered.

When using backed enums, there MUST NOT be a space between the enum name and 
colon, and there must be exactly one space between the colon and the backing
type, e.g. "enum Suit: string" or "enum BanExpiry: int".

Enum case declarations MUST use PascalCase capitalization. Enum case
declarations MUST be on their own line.

An example of this can be seen in the online php documentation at https://www.php.net/manual/en/language.enumerations.backed.php

    <?php
    enum Suit: string
    {
        case Hearts = 'H';
        case Diamonds = 'D';
        case Clubs = 'C';
        case Spades = 'S';
    }
    ?>

Constants in Enums MAY be either PascalCase or UPPER_CASE, PascalCase
is RECOMMENDED, so that it is consistent with case declarations.

    <?php
    enum Size
    {
        case Small;
        case Medium;
        case Large;
    
        public const Huge = self::Large;
    }
    ?>

## [Section 10 - Heredoc and Nowdoc](https://www.php-fig.org/per/coding-style/#10-heredoc-and-nowdoc)

This is a new section about HereDocs and NowDocs.

NowDoc SHOULD be used whereever possible. Heredoc MAY be used where a
nowdoc is not sufficient.

Declared heredocs or nowdocs MUST begin on the same line as the context
the declaration is being used in. Subsequent lines in the heredoc
or nowdoc MUST be indented once past the scope indentation they are
declared in.

The heredoc MUST be declared on the same line as the variable declaration it's being set against.
The heredoc MUST be indented once past the indentation of the scope it's declared in.

## [Section 11 - Arrays](https://www.php-fig.org/per/coding-style/#11-arrays)

This is a new section.

Arrays MUST be declared using the short array syntax.
Arrays MUST follow the trailing comma guidelines.

Array declarations MAY be split across multiple lines, where each
subsequent line is indented once. When doing so, the first value in the
array MUST be on the next line, and there MUST be only one value per line.

When the array declaration is split across multiple lines, the opening
bracket MUST be placed on the same line as the equals sign. 

The closing bracket MUST be placed on the next line after the last value. 

There MUST NOT be more than one value assignment per line. 

Value assignments MAY use a single line or multiple lines.

## [Section 12 - Attributes](https://www.php-fig.org/per/coding-style/#12-attributes)

This is a new section.

Attribute names MUST immediately follow the opening attribute block indicator #[ with no space.

If an attribute has no arguments, the () MUST be omitted.

The closing attribute block indicator ] MUST follow the last character
of the attribute name or the closing ) of its argument list, with no
preceding space.

The construct #[...] is referred to as an "attribute block" in this document.

Attributes on classes, methods, functions, constants and properties
MUST be placed on their own line, immediately prior to the structure
being described.

For attributes on parameters, if the parameter list is presented on a
single line, the attribute MUST be placed inline with the parameter it
describes, separated by a single space. If the parameter list is split
into multiple lines for any reason, the attribute MUST be placed on its
own line prior to the parameter, indented the same as the parameter. If
the parameter list is split into multiple lines, a blank line MAY be
included between one parameter and the attributes of the following
parameter in order to aid readability.

If a comment docblock is present on a structure that also includes an
attribute, the comment block MUST come first, followed by any attributes,
followed by the structure itself. There MUST NOT be any blank lines
between the docblock and attributes, or the attributes and the structure.

If two separate attribute blocks are used in a multi-line context,
they MUST be on separate lines with no blank lines between them.

 * If multiple attributes are placed in the same attribute block, they MUST be separated by a comma with a space following but no space preceding. 
 * If the attribute list is split into multiple lines for any reason, then the attributes MUST be placed in separate attribute blocks. Those blocks may themselves contain multiple attributes provided this rule is respected.

If an attribute's argument list is split into multiple lines for any reason, then:

 * The attribute MUST be the only one in its attribute block.
 * The attribute arguments MUST follow the same rules as defined for multiline function calls.

