# Migrating from PER-CS v1.0 (PSR-12) to PER-CS v2.0 ###

## Summary

PER-CS is the next evolution of the PSR set of Coding Standards from the
PHP-FIG (Framework Interoperability Group). It extends the Coding Standards
laid out in PSR-12 to the newest functionality added to PHP such as the match
keyword, enums, attributes, and more.

This document describes the changes and additions on a section by section
basis between PER-CS v2.0 and PER-CS v1.0 (which is a direct equivalent of 
PSR12 with very minor changes).

It is derived in part from [a GitHub-generated diff](https://github.com/php-fig/per-coding-style/compare/1.0.0...2.0.0#files_bucket)
and focuses on the changes on a section-by-section basis as its focus is to be more readable.

This document intends to provide a summary of these changes that can
then be used to drive action lists for toolset producers to support PER-CS v2.0.

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

[abstract|final] [public|protected|private] [static] [readonly] [type] name

Furthermore, all keywords must be on a single line and MUST be separated
by a single space.

## [Section 4.7 - Method and Function Calls](https://www.php-fig.org/per/coding-style/#47-method-and-function-calls)

If using named arguments, there MUST NOT be a space between the argument name and the colon, 
and there MUST be a single space between the colon and the argument value.

Method chaining MAY be put on separate lines, where each subsequent line is indented once. When doing so, the first method MUST be on the next line.

## [Section 4.8 - Function Callable References](https://www.php-fig.org/per/coding-style/#48-function-callable-references)

Function callable references - there must not be whitespace surrounding the '...' operator ()

## [Section 5.2 - Switch, Case, Match](https://www.php-fig.org/per/coding-style/#52-switch-case-match)

The match keyword is now covered.

## [Section 7.1 - Short Closures](https://www.php-fig.org/per/coding-style/#71-short-closures)

A new subsection about Short Closures, as per the link above. Example as follows:

    <?php
    $func = fn(int $x, int $y): int => $x + $y;

    $func = fn(int $x, int $y): int
        => $x + $y;

    $func = fn(
        int $x,
        int $y,
    ): int
        => $x + $y;

    $result = $collection->reduce(fn(int $x, int $y): int => $x + $y, 0);
    ?>

## [Section 9 - Enumerations](https://www.php-fig.org/per/coding-style/#9-enumerations)

Enums are now covered, as per the link above. Please see below for examples.

    <?php
    enum Suit: string
    {
        case Hearts = 'H';
        case Diamonds = 'D';
        case Clubs = 'C';
        case Spades = 'S';
    }
    ?>

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

This is a new section about Heredoc and Nowdoc notation as per the link above.
Example follows:

    function allowed()
    {
        $allowedHeredoc = <<<COMPLIANT
            This
            is
            a
            compliant
            heredoc
            COMPLIANT;

        $allowedNowdoc = <<<'COMPLIANT'
            This
            is
            a
            compliant
            nowdoc
            COMPLIANT;

        var_dump(
            'foo',
            <<<'COMPLIANT'
                This
                is
                a
                compliant
                parameter
                COMPLIANT,
            'bar',
        );
    }

## [Section 11 - Arrays](https://www.php-fig.org/per/coding-style/#11-arrays)

This is a new section about arrays, as per the link above.
Example as follows:

    <?php
    $arr1 = ['single', 'line', 'declaration'];
    $arr2 = [
        'multi',
        'line',
        'declaration',
        ['values' => 1, 5, 7],
        [
            'nested',
            'array',
        ],
    ];

## [Section 12 - Attributes](https://www.php-fig.org/per/coding-style/#12-attributes)

This is a new section, as per the above link.
The following is an example of valid usage.

    #[Foo]
    #[Bar('baz')]
    class Demo
    {
        #[Beep]
        private Foo $foo;

        public function __construct(
            #[Load(context: 'foo', bar: true)]
            private readonly FooService $fooService,

            #[LoadProxy(context: 'bar')]
            private readonly BarService $barService,
        ) {}

        /**
        * Sets the foo.
        */
        #[Poink('narf'), Narf('poink')]
        public function setFoo(#[Beep] Foo $new): void
        {
        // ...
        }

        #[Complex(
            prop: 'val',
            other: 5,
        )]
        #[Other, Stuff]
        #[Here]
        public function complicated(
            string $a,

            #[Decl]
            string $b,

            #[Complex(
                prop: 'val',
                other: 5,
            )]
            string $c,

            int $d,
        ): string {
            // ...
        }
    }
