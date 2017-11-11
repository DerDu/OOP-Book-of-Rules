# 01 - Coding Standards - PSR-1 & PSR-2

This guide extends and expands on PSR-1 / PSR-2 coding standard.

The intent of this guide is to reduce cognitive friction when scanning code from different authors. It does so by enumerating a shared set of rules and expectations about how to format PHP code.

## 1. Files

### 1.1. PHP Tags

- Files MUST use only `<?php` tags.

- The closing ?> tag MUST be omitted from files containing only PHP.

- It MUST NOT use the other tag variations.

### 1.2. Character Encoding

- Files MUST use only UTF-8 without BOM for PHP code.

- All PHP files MUST use the Unix LF (linefeed) line ending.

### 1.3. Side Effects

A file SHOULD declare new symbols (classes, functions, constants,
etc.) and cause no other side effects, or it SHOULD execute logic with side
effects, but SHOULD NOT do both.

The phrase "side effects" means execution of logic not directly related to
declaring classes, functions, constants, etc., *merely from including the
file*.

"Side effects" include but are not limited to: generating output, explicit
use of `require` or `include`, connecting to external services, modifying ini
settings, emitting errors or exceptions, modifying global or static variables,
reading from or writing to a file, and so on.

The following is an example of a file with both declarations and side effects;
i.e, an example of what to avoid:

~~~php
<?php
// side effect: change ini settings
ini_set('error_reporting', E_ALL);

// side effect: loads a file
include "file.php";

// side effect: generates output
echo "<html>\n";

// declaration
function foo()
{
    // function body
}
~~~

The following example is of a file that contains declarations without side
effects; i.e., an example of what to emulate:

~~~php
<?php
// declaration
function foo()
{
    // function body
}

// conditional declaration is *not* a side effect
if (! function_exists('bar')) {
    function bar()
    {
        // function body
    }
}
~~~


## 2. Source Code

### 2.1. File specific

- Code MUST use 4 spaces for indenting, not tabs.

- There MUST NOT be a hard limit on line length; the soft limit MUST be 120 characters; lines SHOULD be 80 characters or less.

- There MUST be one blank line after the namespace declaration, and there MUST be one blank line after the block of use declarations.

- All PHP files MUST end with a single blank line.

- There MUST NOT be trailing whitespace at the end of non-blank lines.

- Blank lines MAY be added to improve readability and to indicate related blocks of code.

### 2.2. Code specific

- Opening braces for classes MUST go on the next line, and closing braces MUST go on the next line after the body.

- Opening braces for methods MUST go on the next line, and closing braces MUST go on the next line after the body.

- Visibility MUST be declared on all properties and methods; abstract and final MUST be declared before the visibility; static MUST be declared after the visibility.

- Control structure keywords MUST have one space after them; method and function calls MUST NOT.

- Opening braces for control structures MUST go on the same line, and closing braces MUST go on the next line after the body.

- Opening parentheses for control structures MUST NOT have a space after them, and closing parentheses for control structures MUST NOT have a space before.

- There MUST NOT be more than one statement per line.

- PHP keywords MUST be in lower case.

- The PHP constants true, false, and null MUST be in lower case.

## 3. Namespace and Class Names

- Namespaces and classes MUST follow an "autoloading" PSR: PSR-4

This means each class is in a file by itself, and is in a namespace of at
least one level: a top-level vendor name.

### 3.1. General

- Class names MUST be declared in `StudlyCaps`.

- Code written for PHP 5.3 and after MUST use formal namespaces.

For example:

~~~php
<?php
// PHP 5.3 and later:
namespace Vendor\Model;

class Foo
{
}
~~~

### 3.2. Use Declarations

- When present, there MUST be one blank line after the `namespace` declaration.

- When present, all `use` declarations MUST go after the `namespace`
declaration.

- There MUST be one `use` keyword per declaration.

- There MUST be one blank line after the `use` block.

For example:

~~~php
<?php
namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

// ... additional PHP code ...

~~~

## 4. Class Constants, Properties, and Methods

The term "class" refers to all classes, interfaces, and traits.

### 4.1. Constants

Class constants MUST be declared in all upper case with underscore separators.
For example:

~~~php
<?php
namespace Vendor\Model;

class Foo
{
    const VERSION = '1.0';
    const DATE_APPROVED = '2012-06-01';
}
~~~

### 4.2. Properties

This section intentionally avoids any recommendation regarding the use of
`$StudlyCaps`, `$camelCase`, or `$under_score` property names.

Whatever naming convention is used SHOULD be applied consistently within a
reasonable scope. That scope may be vendor-level, package-level, class-level,
or method-level.

### 4.3. Methods

Method names MUST be declared in `camelCase()`.
