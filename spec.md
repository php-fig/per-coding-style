# Coding Style Guide

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL
NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED",
"MAY", and "OPTIONAL" in this document are to be interpreted as
described in [BCP 14][] [[RFC 2119][]] [[RFC 8174][]] when, and only when, they
appear in all capitals, as shown here.

[BCP 14]: https://datatracker.ietf.org/doc/html/bcp14/
[RFC 2119]: https://datatracker.ietf.org/doc/html/rfc2119
[RFC 8174]: https://datatracker.ietf.org/doc/html/rfc8174

## Overview

This specification extends, expands and replaces [PSR-12][], the extended coding style guide and
requires adherence to [PSR-1][], the basic coding standard.

Like [PSR-12][], the intent of this specification is to reduce cognitive friction when
scanning code from different authors. It does so by enumerating a shared set of rules
and expectations about how to format PHP code. This Standard seeks to provide a set that
coding style tools can implement, projects can declare adherence to and developers
can easily relate to between different projects. When various authors collaborate
across multiple projects, it helps to have one set of guidelines to be used among
all those projects. Thus, the benefit of this guide is not in the rules themselves
but the sharing of those rules.

[PSR-12][] was accepted in 2019 and since then a number of changes have been made to PHP
which have implications for coding style guidelines. Whilst [PSR-12] is very comprehensive
of PHP functionality that existed at the time of writing, new functionality is very
open to interpretation. This PER, therefore, seeks to clarify the content of PSR-12 in
a more modern context with new functionality available, make the errata to PSR-12
binding and further update it according to new data and language changes.

### Previous language versions

Throughout this document, any instructions MAY be ignored if they do not exist in versions
of PHP supported by your project.

### Example

This example encompasses some rules below as a quick overview:

```php
<?php

declare(strict_types=1);

namespace Vendor\Package;

use Vendor\Package\{ClassA as A, ClassB, ClassC as C};
use Vendor\Package\SomeNamespace\ClassD as D;

use function Vendor\Package\{functionA, functionB, functionC};

use const Vendor\Package\{ConstantA, ConstantB, ConstantC};

class Foo extends Bar implements FooInterface
{
    public function sampleFunction(int $a, int $b = null): array
    {
        if ($a === $b) {
            bar();
        } elseif ($a > $b) {
            $foo->bar($arg1);
        } else {
            BazClass::bar($arg2, $arg3);
        }
    }

    final public static function bar()
    {
        // ...
    }
}

enum Beep: int
{
    case Foo = 1;
    case Bar = 2;

    public function isOdd(): bool
    {
        return $this->value() % 2;
    }
}
```

## 2. General

### 2.1 Basic Coding Standard

Code MUST follow all rules outlined in [PSR-1].

The term "StudlyCaps" in PSR-1 MUST be interpreted as PascalCase where the first letter of
each word is capitalized including the very first letter.

### 2.2 Files

All PHP files MUST use the Unix LF (linefeed) line ending only.

All PHP files MUST end with a non-blank line, terminated with a single LF.

The closing `?>` tag MUST be omitted from files containing only PHP.

### 2.3 Lines

There MUST NOT be a hard limit on line length.

The soft limit on line length MUST be 120 characters.

Lines SHOULD NOT be longer than 80 characters; lines longer than that SHOULD
be split into multiple subsequent lines of no more than 80 characters each.

There MUST NOT be trailing whitespace at the end of lines.

Blank lines MAY be added to improve readability and to indicate related
blocks of code except where explicitly forbidden.

There MUST NOT be more than one statement per line.

### 2.4 Indenting

Code MUST use an indent of 4 spaces for each indent level, and MUST NOT use
tabs for indenting.

### 2.5 Keywords and Types

All PHP reserved keywords and types [[1]][keywords][[2]][types] MUST be in lower case.

Any new types and keywords added to future PHP versions MUST be in lower case.

Short form of type keywords MUST be used i.e. `bool` instead of `boolean`,
`int` instead of `integer` etc.

Compound types includes intersection, union, and mixed intersection and union type declarations. PHP requires
that all compound types be structured as an ORed (unioned) series of ANDs (intersections), and that each set of
intersections be encased with parentheses.

The union symbol `|` and intersection symbol `&` MUST NOT have a leading or trailing space.  The parentheses MUST NOT
have a leading or trailing space.

If it is necessary to split a compound type into multiple lines:

* If the type contains only intersections or only unions, then each line MUST have a single type.
* If the type contains both intersections and unions, then each line MUST have a single union segment. All intersections in a segment MUST be on the same line.
* The symbol on which the compound type is split MUST be at the start of each line.

The following are correct ways to format compound types:

```php
function foo(int|string $a): User|Product
{
    // ...
}

function somethingWithReflection(
    \ReflectionObject
    |\ReflectionClass
    |\ReflectionMethod
    |\ReflectionParameter
    |\ReflectionProperty $reflect
): object|null {
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

If one of the ORed conditions is `null`, it MUST be the last item in the list.

An intersection of a single simple type with `null` SHOULD be abbreviated using the `?` alternate syntax: `?T`.

### 2.6 Trailing commas

Numerous PHP constructs allow a sequence of values to be separated by a comma,
and the final item may have an optional comma. Examples include array key/value pairs,
function arguments, closure `use` statements, `match()` statement branches, etc.

If that list is contained on a single line, then the last item MUST NOT have a trailing comma.

If the list is split across multiple lines, then the last item MUST have a trailing comma.

The following are examples of correct comma placement:

```php
function beep(string $a, string $b, string $c)
{
    // ...
}

function beep(
    string $a,
    string $b,
    string $c,
) {
    // ...
}

$arr = ['a' => 'A', 'b' => 'B', 'c' => 'C'];

$arr = [
    'a' => 'A',
    'b' => 'B',
    'c' => 'C',
];

$result = match ($a) {
    'foo' => 'Foo',
    'bar' => 'Bar',
    default => 'Baz',
};
```

### 2.7 Naming

This Standard RECOMMENDS following the [php-src coding standards](https://github.com/php/php-src/blob/master/CODING_STANDARDS.md#user-functionsmethods-naming-conventions) with regard to abbreviations and acronyms.

Specifically:

> Abbreviations and acronyms as well as initialisms SHOULD be avoided wherever possible, unless they are much more widely used than the long form (e.g. HTTP or URL). Abbreviations, acronyms, and initialisms SHOULD be treated like regular words, thus they SHOULD be written with an uppercase first character, followed by lowercase characters.

## 3. Declare Statements, Namespace, and Import Statements

The header of a PHP file may consist of a number of different blocks. If present,
each of the blocks below MUST be separated by a single blank line, and MUST NOT contain
a blank line. Each block MUST be in the order listed below, although blocks that are
not relevant may be omitted.

* Opening `<?php` tag.
* File-level docblock.
* One or more declare statements.
* The namespace declaration of the file.
* One or more class-based `use` import statements.
* One or more function-based `use` import statements.
* One or more constant-based `use` import statements.
* The remainder of the code in the file.

When a file contains a mix of HTML and PHP, any of the above sections may still
be used. If so, they MUST be present at the top of the file, even if the
remainder of the code consists of a closing PHP tag and then a mixture of HTML and
PHP.

When the opening `<?php` tag is on the first line of the file, it MUST be on its
own line with no other statements unless it is a file containing markup outside of PHP
opening and closing tags.  The `<?php` tag MUST always be lower case.

Import statements MUST never begin with a leading backslash as they
must always be fully qualified.

The following example illustrates a complete list of all blocks:

```php
<?php

/**
 * This file contains an example of coding styles.
 */

declare(strict_types=1);

namespace Vendor\Package;

use Vendor\Package\{ClassA as A, ClassB, ClassC as C};
use Vendor\Package\SomeNamespace\ClassD as D;
use Vendor\Package\AnotherNamespace\ClassE as E;
use SomeVendor\Pack\ANamespace\SubNamespace\ClassF;

use function Vendor\Package\{functionA, functionB, functionC};
use function Another\Vendor\functionD;

use const Vendor\Package\{CONSTANT_A, CONSTANT_B, CONSTANT_C};
use const Another\Vendor\CONSTANT_D;

/**
 * FooBar is an example class.
 */
class FooBar
{
    // ...
}
```

When using compound namespaces, there MUST NOT be more than two sub-namespaces within the group.
That is, the following is allowed:

```php
<?php

use Vendor\Package\SomeNamespace\{
    SubnamespaceOne\ClassA,
    SubnamespaceOne\ClassB,
    SubnamespaceTwo\ClassY,
    ClassZ,
};
```

And the following would not be allowed:

```php
<?php

use Vendor\Package\SomeNamespace\{
    // This has too many namespace segments to be in a group
    SubnamespaceOne\AnotherNamespace\ClassA,
    SubnamespaceOne\ClassB,
    ClassZ,
};
```

When wishing to declare strict types in files containing markup outside PHP
opening and closing tags, the declaration MUST be on the first line of the file
and include an opening PHP tag, the strict types declaration and closing tag.

For example:

```php
<?php declare(strict_types=1) ?>
<html>
<body>
    <?php
        // ...
    ?>
</body>
</html>
```

Declare statements MUST NOT contain any spaces and MUST be exactly `declare(strict_types=1)`
(with an optional semicolon terminator).

Block declare statements are allowed and MUST be formatted as below. Note position of
braces and spacing:

```php
declare(ticks=1) {
    // ...
}
```

## 4. Classes, Properties, and Methods

The term "class" refers to all classes, interfaces, traits, and enums.

Any closing brace MUST NOT be followed by any comment or statement on the
same line.

When instantiating a new class, parentheses MUST always be present even when
there are no arguments passed to the constructor. For example:

```php
new Foo();
```

If class contains no additional declarations (such as an exception that exists only to extend another exception with a new type),
then the body of the class SHOULD be abbreviated as `{}` and placed on the same line as the previous symbol,
separated by a space. For example:

```php
class MyException extends \RuntimeException {}
```

When accessing a class member immediately after instantiating a new class, the instantiation SHOULD NOT be wrapped in 
parentheses. For example:

```php
new Foo()->someMethod();
new Foo()::someStaticMethod();
new Foo()->someProperty;
new Foo()::$someStaticProperty;
new Foo()::SOME_CONSTANT;
```

And the following SHOULD be avoided:

```php
(new Foo())->someMethod();
```

### 4.1 Extends and Implements

The `extends` and `implements` keywords MUST be declared on the same line as
the class name.

The opening brace for the class MUST go on its own line, and MUST NOT be
preceded or followed by a blank line.

The closing brace for the class MUST go on its own line, immediately following
the last line of the class body, and MUST NOT be preceded by a blank line.

The following is a validly formatted class:

```php
<?php

namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class ClassName extends ParentClass implements \ArrayAccess, \Countable
{
    // ...
}
```

Lists of `implements` and, in the case of interfaces, `extends` MAY be split
across multiple lines, where each subsequent line is indented once. When doing
so, the first item in the list MUST be on the next line, and there MUST be only
one interface per line. For example:

```php
<?php

namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class ClassName extends ParentClass implements
    \ArrayAccess,
    \Countable,
    \Serializable
{
    // ...
}
```

### 4.2 Using traits

The `use` keyword used inside the classes to implement traits MUST be
declared on the next line after the opening brace.

Each individual trait that is imported into a class MUST be included
one-per-line and each inclusion MUST have its own `use` import statement.

The following is a correct example of trait usage.

```php
<?php

namespace Vendor\Package;

use Vendor\Package\FirstTrait;
use Vendor\Package\SecondTrait;
use Vendor\Package\ThirdTrait;

class ClassName
{
    use FirstTrait;
    use SecondTrait;
    use ThirdTrait;
}
```

When the class has nothing after the `use` import statement, the class
closing brace MUST be on the next line after the `use` import statement.
For example:

```php
<?php

namespace Vendor\Package;

use Vendor\Package\FirstTrait;

class ClassName
{
    use FirstTrait;
}
```

Otherwise, it MUST have a blank line after the `use` import statement, as in:

```php
<?php

namespace Vendor\Package;

use Vendor\Package\FirstTrait;

class ClassName
{
    use FirstTrait;

    private $property;
}
```

When using the `insteadof` and `as` operators they MUST be used as follows taking
note of indentation, spacing, and new lines.

```php
<?php

class Talker
{
    use A;
    use B {
        A::smallTalk insteadof B;
    }
    use C {
        B::bigTalk insteadof C;
        C::mediumTalk as FooBar;
    }
}
```

### 4.3 Properties and Constants

Visibility MUST be declared on all properties.  If set-visibility is specified, then the general visibility MAY be omitted.

Visibility MUST be declared on all constants.

The `var` keyword MUST NOT be used to declare a property.

There MUST NOT be more than one property or constant declared per statement.

Property or constant names MUST NOT be prefixed with a single underscore to indicate
protected or private visibility. That is, an underscore prefix explicitly has
no meaning.

There MUST be a space between type declaration and property name.

A property declaration looks like the following:

```php
<?php

namespace Vendor\Package;

class ClassName
{
    public $foo = null;
    public static int $bar = 0;
}
```

### 4.4 Methods and Functions

Visibility MUST be declared on all methods.

Method names MUST NOT be prefixed with a single underscore to indicate
protected or private visibility. That is, an underscore prefix explicitly has
no meaning.

Method and function names MUST NOT be declared with space after the method name. The
opening brace MUST go on its own line, and the closing brace MUST go on the
next line following the body. There MUST NOT be a space after the opening
parenthesis, and there MUST NOT be a space before the closing parenthesis.

A method declaration looks like the following. Note the placement of
parentheses, commas, spaces, and braces:

```php
<?php

namespace Vendor\Package;

class ClassName
{
    public function fooBarBaz($arg1, &$arg2, $arg3 = [])
    {
        // ...
    }
}
```

A function declaration looks like the following. Note the placement of
parentheses, commas, spaces, and braces:

```php
<?php

function fooBarBaz($arg1, &$arg2, $arg3 = [])
{
    // ...
}
```

If a function or method contains no statements or comments (such as an empty no-op implementation or when using
constructor property promotion), then the body SHOULD be abbreviated as `{}` and placed on the same
line as the previous symbol, separated by a space. For example:

```php
class Point
{
    public function __construct(private int $x, private int $y) {}
    
    // ...
}
```

```php
class Point
{
    public function __construct(
      public readonly int $x,
      public readonly int $y,
    ) {}
}
```

### 4.5 Method and Function Parameters

In the argument list, there MUST NOT be a space before each comma, and there
MUST be one space after each comma.

Method and function parameters with default values MUST go at the end of the argument
list. For example:

```php
<?php

namespace Vendor\Package;

class ClassName
{
    public function foo(int $arg1, &$arg2, $arg3 = [])
    {
        // ...
    }
}
```

Argument lists MAY be split across multiple lines, where each subsequent line
is indented once. When doing so, the first item in the list MUST be on the
next line, and there MUST be only one argument per line.

When the argument list is split across multiple lines, the closing parenthesis
and opening brace MUST be placed together on their own line with one space
between them. For example:

```php
<?php

namespace Vendor\Package;

class ClassName
{
    public function aVeryLongMethodName(
        ClassTypeHint $arg1,
        &$arg2,
        array $arg3 = [],
    ) {
        // ...
    }
}
```

When you have a return type declaration present, there MUST be one space after
the colon followed by the type declaration. The colon and declaration MUST be
on the same line as the argument list closing parenthesis with no spaces between
the two characters. For example:

```php
<?php

declare(strict_types=1);

namespace Vendor\Package;

class ReturnTypeVariations
{
    public function functionName(int $arg1, $arg2): string
    {
        return 'foo';
    }

    public function anotherFunction(
        string $foo,
        string $bar,
        int $baz,
    ): string {
        return 'foo';
    }
}
```

In nullable type declarations, there MUST NOT be a space between the question mark
and the type. For example:

```php
<?php

declare(strict_types=1);

namespace Vendor\Package;

class ReturnTypeVariations
{
    public function functionName(?string $arg1, ?int &$arg2): ?string
    {
        return 'foo';
    }
}
```

When using the reference operator `&` before an argument, there MUST NOT be
a space after it, like in the previous example.

There MUST NOT be a space between the variadic three dot operator and the argument
name:

```php
public function process(string $algorithm, ...$parts)
{
    // ...
}
```

When combining both the reference operator and the variadic three dot operator,
there MUST NOT be any space between the two of them:

```php
public function process(string $algorithm, &...$parts)
{
    // ...
}
```

### 4.6 Modifier Keywords

Classes, properties, and methods have numerous keyword modifiers that alter how the
engine and language handles them. When present, they MUST be in the following order:

* Inheritance modifier: `abstract` or `final`
* Visibility modifier: `public`, `protected`, or `private`
* Set-visibility modifier: `public(set)`, `protected(set)`, or `private(set)`
* Scope modifier: `static`
* Mutation modifier: `readonly`
* Type declaration
* Name

All keywords MUST be on a single line, and MUST be separated by a single space.  All keywords MUST be all lower-case.  The `public` keyword MAY be omitted when using a set-visibility on a public-read property.

The following is a correct example of modifier keyword usage:

```php
<?php

namespace Vendor\Package;

abstract class ClassName
{
    protected static string $foo;

    private readonly int $beep;

    protected private(set) string $name;

    protected(set) string $boop;

    abstract protected function zim();

    final public static function bar()
    {
        // ...
    }
}

readonly class ValueObject
{
    // ...
}
```

### 4.7 Method and Function Calls

When making a method or function call, there MUST NOT be a space between the
method or function name and the opening parenthesis, there MUST NOT be a space
after the opening parenthesis, and there MUST NOT be a space before the
closing parenthesis. In the argument list, there MUST NOT be a space before
each comma, and there MUST be one space after each comma.

The following lines show correct calls:

```php
<?php

bar();
$foo->bar($arg1);
Foo::bar($arg2, $arg3);
```

Argument lists MAY be split across multiple lines, where each subsequent line
is indented once. When doing so, the first item in the list MUST be on the
next line, and there MUST be only one argument per line. A single argument being
split across multiple lines (as might be the case with a closure or
array) does not constitute splitting the argument list itself.

The following examples show correct argument usage.

```php
<?php

$foo->bar(
    $longArgument,
    $longerArgument,
    $muchLongerArgument,
);
```

```php
<?php

somefunction($foo, $bar, [
  // ...
], $baz);

$app->get('/hello/{name}', function ($name) use ($app) {
    return 'Hello ' . $app->escape($name);
});
```

If using named arguments, there MUST NOT be a space between the argument name
and colon, and there MUST be a single space between the colon and the argument value. For example:

```php
somefunction($a, b: $b, c: 'c');
```

Method chaining MAY be put on separate lines, where each subsequent line is indented once. When doing so, the first
method MUST be on the next line. For example:

```php
$someInstance
    ->create()
    ->prepare()
    ->run();
```

The `exit()` and `die()` functions SHOULD always be called with parentheses even if no argument is given to clearly
distinguish them from an access to a constant named `exit` or `die`. For example:

```php
exit();
exit(1);
exit("Success!");
die();

$result = foo() ?? exit();
```

### 4.8 Function Callable References

A function or method may be referenced in a way that creates a closure out of it, by providing `...` in place of arguments.

If so, the `...` MUST NOT include any whitespace before or after. That is, the correct format is `foo(...)`.

### 4.9 Property Hooks

Object properties may also include hooks, which have a number of syntactic options.

When using the long form of hooks:

* The opening brace MUST be on the same line as the property.
* The opening brace MUST be separated from the property name or its default value by a single space.
* The closing brace MUST be on its own line, and have no comment following it.
* The entire body of the hook definition MUST be indented one level.
* The body of each hook MUST be indented one level.
* If multiple hooks are declared, they MUST be separated by at least a single line break.  They
  MAY be separated by an additional blank line to aid readability.

For example:

```php
class Example
{
    public string $newName = 'Me' {
        set(string $value) {
            if (strlen($value) < 3) {
                throw new \Exception('Too short');
            }
            $this->newName = ucfirst($value);
        }
    }

    public string $department {
        get {
            return $this->values[__PROPERTY__];
        }
        set {
            $this->values[__PROPERTY__] = $value;
        }
    }
    // or
    public string $department {
        get {
            return $this->values[__PROPERTY__];
        }

        set {
            $this->values[__PROPERTY__] = $value;
        }
    }
}
```

Property hooks also support multiple short-hook variations.

For a `set` hook, if the argument name and type do not need to be redefined, then they MAY be omitted.

If a hook consists of a single expression, then PHP allows it to be shortened using `=>`.  In that case:

* There MUST be a single space on either side of the `=>` symbol.
* The body MUST begin on the same line as the hook name and `=>`.
* Wrapping is allowed if the expression used allows for wrapping, using the rules defined elsewhere in this document.

```php
class Example
{
    public string $myName {
        get => __CLASS__;
    }

    public string $newName {
        set => ucfirst($value);
    }
}
```

Additionally, if the following criteria are met:

* There is only one hook implementation.
* That hook uses the short-hook syntax.
* That hook expression does not contain any wrapping.

Then the hook MAY be listed entirely inline.  In that case,

* The hook name MUST be separated from the opening brace and the arrow operator by a single space
* The semicolon ending of the hook MUST be separated from the closing brace by a single space.

For example:

```php
class Example
{
    public string $myName { get => __CLASS__; }

    public string $newName { set => ucfirst($value); }
}
```

Property hooks MAY also be defined in constructor-promoted properties.  However, they
MUST be only a single hook, with a short-syntax body, defined on a single line as above.
If those criteria are not met, then the promoted property MUST NOT have any hooks defined
inline.

```php
class Example
{
    public function __construct(
        public string $name { set => ucfirst($value); }
    ) {}
}
```

The following is ***not allowed*** due to the hook being too complex:

```php
class Example
{
    public function __construct(
        public string $name {
            set {
                if (strlen($value) < 3) {
                    throw new \Exception('Too short');
                }
                $this->newName = ucfirst($value);
            }
        }
    ) {}
}
```

## 4.10 Interface and abstract properties

Abstract properties may be defined in interfaces or abstract classes, but are required to
specify if they must support `get` operations, `set` operations, or both.  In the case
of abstract classes, they MAY include a body for one or another hook.

If there is a body for any hook, then the entire hook block MUST follow
the same rules as for defined hooks above.  The only difference is that
a hook that has no body specified have a single semicolon after the hook
keyword, with no space before it.

```php
abstract class Example {
    abstract public string $name {
        get => ucfirst($this->name);
        set;
    }
}
```

If there is no body for either hook, then the following rules apply:

* The operation block MUST be on the same line as the property.
* There MUST be a single space between the property name and the operation block `{}`.
* There MUST be a single space after the opening `{`.
* There MUST be a single space before the closing `}`;
* There MUST NOT be a space between the operation and its required semicolon.
* If multiple operations are specified, they MUST be separated by a single space.
* The `get` operation MUST be listed before the `set` operation.

```php
interface Example
{
    public string $readable { get; }

    public string $writeable { set; }

    public string $both { get; set; }
}
```

## 5. Control Structures

The general style rules for control structures are as follows:

- There MUST be one space after the control structure keyword
- There MUST NOT be a space after the opening parenthesis
- There MUST NOT be a space before the closing parenthesis
- There MUST be one space between the closing parenthesis and the opening
  brace
- The structure body MUST be indented once
- The body MUST be on the next line after the opening brace
- The closing brace MUST be on the next line after the body

The body of each structure MUST be enclosed by braces. This standardizes how
the structures look and reduces the likelihood of introducing errors as new
lines get added to the body.

### 5.1 `if`, `elseif`, `else`

An `if` structure looks like the following. Note the placement of parentheses,
spaces, and braces; and that `else` and `elseif` are on the same line as the
closing brace from the earlier body.

```php
<?php

if ($expr1) {
    // ...
} elseif ($expr2) {
    // ...
} else {
    // ...
}
```

The keyword `elseif` SHOULD be used instead of `else if` so that all control
keywords look like single words.

Expressions in parentheses MAY be split across multiple lines, where each
subsequent line is indented at least once. When doing so, the first condition
MUST be on the next line. The closing parenthesis and opening brace MUST be
placed together on their own line with one space between them. Boolean
operators between conditions MUST always be at the beginning. For example:

```php
<?php

if (
    $expr1
    && $expr2
) {
    // ...
} elseif (
    $expr3
    && $expr4
) {
    // ...
}
```

### 5.2 `switch`, `case`, `match`

A `switch` structure looks like the following. Note the placement of
parentheses, spaces, and braces. The `case` statement MUST be indented once
from `switch`, and the `break` keyword (or other terminating keywords) MUST be
indented at the same level as the `case` body. There MUST be a comment such as
`// no break` when fall-through is intentional in a non-empty `case` body.

```php
<?php

switch ($expr) {
    case 0:
        echo 'First case, with a break';
        break;
    case 1:
        echo 'Second case, which falls through';
        // no break
    case 2:
    case 3:
    case 4:
        echo 'Third case, return instead of break';
        return;
    default:
        echo 'Default case';
        break;
}
```

Expressions in parentheses MAY be split across multiple lines, where each
subsequent line is indented at least once. When doing so, the first condition
MUST be on the next line. The closing parenthesis and opening brace MUST be
placed together on their own line with one space between them. Boolean
operators between conditions MUST always be at the beginning. For example:

```php
<?php

switch (
    $expr1
    && $expr2
) {
    // ...
}
```

Similarly, a `match` expression looks like the following. Note the placement
of parentheses, spaces, and braces.

```php
<?php

$returnValue = match ($expr) {
    0 => 'First case',
    1, 2, 3 => multipleCases(),
    default => 'Default case',
};
```

### 5.3 `while`, `do while`

A `while` statement looks like the following. Note the placement of
parentheses, spaces, and braces.

```php
<?php

while ($expr) {
    // ...
}
```

Expressions in parentheses MAY be split across multiple lines, where each
subsequent line is indented at least once. When doing so, the first condition
MUST be on the next line. The closing parenthesis and opening brace MUST be
placed together on their own line with one space between them. Boolean
operators between conditions MUST always be at the beginning.

```php
<?php

while (
    $expr1
    && $expr2
) {
    // ...
}
```

Similarly, a `do while` statement looks like the following. Note the placement
of parentheses, spaces, and braces.

```php
<?php

do {
    // ...
} while ($expr);
```

Expressions in parentheses MAY be split across multiple lines, where each
subsequent line is indented at least once. When doing so, the first condition
MUST be on the next line. Boolean operators between conditions MUST
always be at the beginning. For example:

```php
<?php

do {
    // ...
} while (
    $expr1
    && $expr2
);
```

### 5.4 `for`

A `for` statement looks like the following. Note the placement of parentheses,
spaces, and braces.

```php
<?php

for ($i = 0; $i < 10; $i++) {
    // ...
}
```

Expressions in parentheses MAY be split across multiple lines, where each
subsequent line is indented at least once. When doing so, the first expression
MUST be on the next line. The closing parenthesis and opening brace MUST be
placed together on their own line with one space between them. For example:

```php
<?php

for (
    $i = 0;
    $i < 10;
    $i++
) {
    // ...
}
```

### 5.5 `foreach`

A `foreach` statement looks like the following. Note the placement of
parentheses, spaces, and braces.

```php
<?php

foreach ($iterable as $key => $value) {
    // ...
}
```

### 5.6 `try`, `catch`, `finally`

A `try-catch-finally` block looks like the following. Note the placement of
parentheses, spaces, and braces.

```php
<?php

try {
    // ...
} catch (FirstThrowableType $e) {
    // ...
} catch (OtherThrowableType|AnotherThrowableType $e) {
    // ...
} finally {
    // ...
}
```

## 6. Operators

Style rules for operators are grouped by arity (the number of operands they take).

When space is permitted around an operator, multiple spaces MAY be
used for readability purposes.

All operators not described here are left undefined.

### 6.1. Unary operators

The increment/decrement operators MUST NOT have any space between
the operator and operand:

```php
$i++;
++$j;
```

Type casting operators MUST NOT have any space within the parentheses and MUST be separated from the variable they are
operating on by exactly one space:

```php
$intValue = (int) $input;
```

### 6.2. Binary operators

All binary operators MUST be preceded and followed by at least one space:

```php
if ($a === $b) {
    $foo = $bar ?? $a ?? $b;
} elseif ($a > $b) {
    $foo = $a + $b * $c;
} else {
    $foo = $a |> log(...) |> round(...);
}
```

As of writing, this applies to:

* `** * / % + -` [arithmetic][] operators
* `< <= > >= == != === !== <> <=>` [comparison][] operators
* `= += -= *= **= /= .= %= &= |= ^= <<= >>= ??=` [assignment][] operators
* `<< >> & ^ |` [bitwise][] operators
* `&& || and xor or` [logical][] operators
* `.` [string][] operator ("concatenation")
* `instanceof` [type][] operator
* `|>` [functional][] operator ("pipe")

### 6.3. Ternary operators

The conditional operator, also known simply as the ternary operator, MUST be
preceded and followed by at least one space around both the `?`
and `:` characters:

```php
$variable = $foo ? 'foo' : 'bar';
```

When the middle operand of the conditional operator is omitted, the operator
MUST follow the same style rules as other binary [comparison][] operators:

```php
$variable = $foo ?: 'bar';
```

### 6.4. Operator's placement

A statement that includes an operator MAY be split across multiple lines, where
each subsequent line is indented once. When doing so, the operator MUST be
placed at the beginning of the new line; ternaries MUST occupy 3 lines, never 2.

For example:

```php
<?php

$variable1 = $ternaryOperatorExpr
    ? 'fizz'
    : 'buzz';

$variable2 = $possibleNullableExpr
    ?? 'fallback';

$variable3 = $elvisExpr
    ?: 'qix';

$variable4 = '<foo>'
    |> strtoupper(...)
    |> htmlspecialchars(...);
```

## 7. Closures

Closures, also known as anonymous functions, MUST be declared with a space
after the `function` keyword, and a space before and after the `use` keyword.

The opening brace MUST go on the same line, and the closing brace MUST go on
the next line following the body.

There MUST NOT be a space after the opening parenthesis of the argument list
or variable list, and there MUST NOT be a space before the closing parenthesis
of the argument list or variable list.

In the argument list and variable list, there MUST NOT be a space before each
comma, and there MUST be one space after each comma.

Closure arguments with default values MUST go at the end of the argument
list.

If a return type is present, it MUST follow the same rules as with normal
functions and methods; if the `use` keyword is present, the colon MUST follow
the `use` list closing parentheses with no spaces between the two characters.

A closure declaration looks like the following. Note the placement of
parentheses, commas, spaces, and braces:

```php
<?php

$closureWithArgs = function ($arg1, $arg2) {
    // ...
};

$closureWithArgsAndVars = function ($arg1, $arg2) use ($var1, $var2) {
    // ...
};

$closureWithArgsVarsAndReturn = function ($arg1, $arg2) use ($var1, $var2): bool {
    // ...
};
```

If a closure contains no statements, then the body MUST be abbreviated as `{}` and placed on the same
line as the previous symbol, separated by a space:

```php
$noOpFunction = function () {};
```

If possible, empty-body closures SHOULD be replaced with arrow functions:

```php
$noOpFunction = fn() => null;
```

Argument lists and variable lists MAY be split across multiple lines, where
each subsequent line is indented once. When doing so, the first item in the
list MUST be on the next line, and there MUST be only one argument or variable
per line.

When the ending list (whether of arguments or variables) is split across
multiple lines, the closing parenthesis and opening brace MUST be placed
together on their own line with one space between them.

The following are examples of closures with and without argument lists and
variable lists split across multiple lines.

```php
<?php

$longArgs_noVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument,
) {
   // ...
};

$noArgs_longVars = function () use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3,
) {
   // ...
};

$longArgs_longVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument,
) use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3,
) {
   // ...
};

$longArgs_shortVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument,
) use ($var1) {
   // ...
};

$shortArgs_longVars = function ($arg) use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3,
) {
   // ...
};
```

Note that the formatting rules also apply when the closure is used directly
in a function or method call as an argument.

```php
<?php

$foo->bar(
    $arg1,
    function ($arg2) use ($var1) {
        // ...
    },
    $arg3,
);
```

### 7.1 Short Closures

Short closures, also known as arrow functions, MUST follow the same guidelines
and principles as long closures above, with the following additions.

The `fn` keyword MUST NOT be succeeded by a space.

The `=>` symbol MUST be preceded and succeeded by a space.

The semicolon at the end of the expression MUST NOT be preceded by a space.

The expression portion MAY be split to a subsequent line. If so, the `=>` MUST be included
on the second line, and MUST be indented once.

The following examples show proper common usage of short closures.

```php
$func = fn(int $x, int $y): int => $x + $y;

$func = fn(int $x, int $y): int
    => $x + $y;

$func = fn(
    int $x,
    int $y,
): int
    => $x + $y;

$result = $collection->reduce(fn(int $x, int $y): int => $x + $y, 0);
```

## 8. Anonymous Classes

Anonymous Classes MUST follow the same guidelines and principles as closures
in the above section.

```php
<?php

$instance = new class {};
```

The opening brace MAY be on the same line as the `class` keyword so long as
the list of `implements` interfaces does not wrap. If the list of interfaces
wraps, the brace MUST be placed on the line immediately following the last
interface.

If the anonymous class has no arguments, the `()` after `class` MUST be omitted. For example:

```php
<?php

// Brace on the same line
// No arguments
$instance = new class extends \Foo implements \HandleableInterface {
    // ...
};

// Brace on the next line
// Constructor arguments
$instance = new class ($a) extends \Foo implements
    \ArrayAccess,
    \Countable,
    \Serializable
{
    public function __construct(public int $a)
    {
    }
    // ...
};
```

If an anonymous class has attributes, they MUST be placed starting on the next line after the `new` keyword, indented
once, and otherwise follow the same rules as other attributes specified in section 12. The remaining anonymous class 
declaration after the final attribute MUST keep the same indentation as the attributes:

```php
$example = new
    #[Attribute]
    class {
        ...
    };
```

## 9. Enumerations

Enumerations (enums) MUST follow the same guidelines as classes, except where otherwise noted below.

Methods in enums MUST follow the same guidelines as methods in classes. Non-public methods MUST use `private`
instead of `protected`, as enums do not support inheritance.

When using a backed enum, there MUST NOT be a space between the enum name and colon, and there MUST be exactly one
space between the colon and the backing type. This is consistent with the style for return types.

Enum case declarations MUST use PascalCase capitalization. Enum case declarations MUST be on their own line.

Constants in Enumerations MAY use either PascalCase or UPPER_CASE capitalization. PascalCase is RECOMMENDED,
so that it is consistent with case declarations.

The following example shows a typical valid Enum:

```php
enum Suit: string
{
    case Hearts = 'H';
    case Diamonds = 'D';
    case Spades = 'S';
    case Clubs = 'C';

    public const Wild = self::Spades;
}
```

## 10. Heredoc and Nowdoc

A nowdoc SHOULD be used wherever possible. Heredoc MAY be used when a nowdoc
does not satisfy requirements.

Heredoc and nowdoc syntax is largely governed by PHP requirements with the only
allowed variation being indentation. Declared heredocs or nowdocs MUST
begin on the same line as the context the declaration is being used in.
Subsequent lines in the heredoc or nowdoc MUST be indented once past the scope
indentation they are declared in.

The following is ***not allowed*** due to the heredoc beginning on a
different line than the context it's being declared in:

```php
$notAllowed =
<<<'COUNTEREXAMPLE'
    This
    is
    not
    allowed.
    COUNTEREXAMPLE;
```

Instead, the heredoc MUST be declared on the same line as the variable
declaration it's being set against.

The following is ***not allowed*** due to the scope indention not matching the scope the
heredoc is declared in:

```php
function notAllowed()
{
    $notAllowed = <<<'COUNTEREXAMPLE'
This
is
not
allowed.
COUNTEREXAMPLE;
}
```

Instead, the heredoc MUST be indented once past the indentation of the scope
it's declared in.

The following is an example of both heredocs and nowdocs declared in a
compliant way:

```php
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
```

## 11. Arrays

Arrays MUST be declared using the short array syntax.

```php
<?php

$arr = [];
```

Arrays MUST follow the trailing comma guidelines.

Array declarations MAY be split across multiple lines, where each subsequent line 
is indented once. When doing so, the first value in the array MUST be on the 
next line, and there MUST be only one value per line.

When the array declaration is split across multiple lines, the opening bracket 
MUST be placed on the same line as the equals sign. The closing bracket 
MUST be placed on the next line after the last value. There MUST NOT be more 
than one value assignment per line. Value assignments MAY use a single line
or multiple lines.

The following example shows correct array usage:

```php
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
```

## 12. Attributes

### 12.1 Basics

Attribute names MUST immediately follow the opening attribute block indicator `#[` with no space.

If an attribute has no arguments, the `()` MUST be omitted.

The closing attribute block indicator `]` MUST follow the last character of the attribute name or the closing `)` of
its argument list, with no preceding space.

The construct `#[...]` is referred to as an "attribute block" in this document.

### 12.2 Placement

Attributes on classes, methods, functions, constants and properties MUST
be placed on their own line, immediately prior to the structure being described.

For attributes on parameters, if the parameter list is presented on a single line,
the attribute MUST be placed inline with the parameter it describes, separated by a single space.
If the parameter list is split into multiple lines for any reason, the attribute MUST be placed on
its own line prior to the parameter, indented the same as the parameter. If the parameter list
is split into multiple lines, a blank line MAY be included between one parameter and the attributes
of the following parameter in order to aid readability.

If a comment docblock is present on a structure that also includes an attribute, the comment block MUST
come first, followed by any attributes, followed by the structure itself. There MUST NOT be any blank lines
between the docblock and attributes, or the attributes and the structure.

If two separate attribute blocks are used in a multi-line context, they MUST be on separate lines with no blank
lines between them.

### 12.3 Compound attributes

If multiple attributes are placed in the same attribute block, they MUST be separated by a comma with a space
following but no space preceding. If the attribute list is split into multiple lines for any reason, then the
attributes MUST be placed in separate attribute blocks. Those blocks may themselves contain multiple
attributes provided this rule is respected.

If an attribute's argument list is split into multiple lines for any reason, then:

* The attribute MUST be the only one in its attribute block.
* The attribute arguments MUST follow the same rules as defined for multiline function calls.

### 12.4 Example

The following is an example of valid attribute usage.

```php
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
```

[PSR-1]: https://www.php-fig.org/psr/psr-1/
[PSR-12]: https://www.php-fig.org/psr/psr-12/
[keywords]: https://php.net/manual/en/reserved.keywords.php
[types]: https://php.net/manual/en/reserved.other-reserved-words.php
[arithmetic]: https://php.net/manual/en/language.operators.arithmetic.php
[assignment]: https://php.net/manual/en/language.operators.assignment.php
[comparison]: https://php.net/manual/en/language.operators.comparison.php
[bitwise]: https://php.net/manual/en/language.operators.bitwise.php
[logical]: https://php.net/manual/en/language.operators.logical.php
[string]: https://php.net/manual/en/language.operators.string.php
[type]: https://php.net/manual/en/language.operators.type.php
[functional]: https://php.net/manual/en/language.operators.functional.php
