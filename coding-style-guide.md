# Fullrate Online Coding Style Guide

This guide extends and expands on [PSR-1], the basic coding standard and
[PSR-2], the coding style guide.

The changes to PSR-2 will be defined as the same number as the original
PSR-2 document. Because of this the additions is starting from 8 to
avoid any confusion.

The intent of this guide is to reduce cognitive friction when scanning code
from different authors. It does so by enumerating a shared set of rules and
expectations about how to format PHP code.

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be
interpreted as described in [RFC 2119].

[RFC 2119]: http://www.ietf.org/rfc/rfc2119.txt
[PSR-0]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md
[PSR-1]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-1-basic-coding-standard.md
[PSR-2]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-2-coding-style-guide.md


## 1. Overview

- Code MUST follow the PSR-1 [[PSR-1]] Basic Coding Standard

- Code MUST follow the PSR-2 [[PSR-2]] Coding Style Guide with the following
  changes and additions.

- (change) Code MUST use **tabs** for indenting, not spaces.

- (change) Opening braces for methods MUST go on the **same** line, and closing braces MUST
  go on the next line after the body.

- (new) Variable names MUST be declared in snake_case.

- (new) DocBlocks SHOULD always be defined for classes.

- (new) DocBlocks MUST always be defined for fields and methods.


### 1.1. Example

This example encompasses some of the rules below as a quick overview:

```php
<?php
namespace Vendor\Package;

use FooInterface;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class Foo extends Bar implements FooInterface
{
	public function sampleMethod($a, $b = null) {
		if ($a === $b) {
			bar();
		} elseif ($a > $b) {
			$foo->bar($arg1);
		} else {
			BazClass::bar($arg2, $arg3);
		}
	}

	final public static function bar() {
		// method body
	}
}
```


### 2.4. (change) Indenting

Code MUST use an indent of **one tab**, and MUST NOT use spaces for indenting.

Spaces MAY be used to do fine-grained alignments of chopped up code.
Use tabs for the normal indentation up until the start of the previous line,
and using spaces to do the alignment. This assures the code will stay aligned
when using different sizes for the tab character.

Spaces MUST be used to do inter-line alignments, with code on both sides.

See the following example and note the indentations and spaces represented
with `→` and `·` respectively.

~~~php
<?php
namespace Vendor\Package;

class ClassName
{
→public function fooBarBaz($arg1, &$arg2, $arg3 = []) {
→→$foo····=·'foo';
→→$barbaz·=·'barbaz';

→→return·Bar::factory()
→→··········->withBaz();
→}
}
~~~


### 2.5. (change) Keywords and True/False/Null

PHP [keywords] MUST be in lower case.

The PHP constants `TRUE`, `FALSE`, and `NULL` MUST be in **upper case**.

[keywords]: http://php.net/manual/en/reserved.keywords.php


### 4.3. (change) Methods

Visibility MUST be declared on all methods.

Method names SHOULD NOT be prefixed with a single underscore to indicate
protected or private visibility.

Method names MUST NOT be declared with a space after the method name. The
opening brace MUST go on **the same** line, and the closing brace MUST go on the
next line following the body. There MUST NOT be a space after the opening
parenthesis, and there MUST NOT be a space before the closing parenthesis.

A method declaration looks like the following. Note the placement of
parentheses, commas, spaces, and braces:

~~~php
<?php
namespace Vendor\Package;

class ClassName
{
	public function fooBarBaz($arg1, &$arg2, $arg3 = []) {
		// method body
	}
}
~~~


### 8. (new) Variable naming

Variable names MUST be declared in snake_case.

Variables include global variables, local variables, class fields.

~~~php
<?php
namespace Vendor\Package;

class ClassName
{
	private $foo_bar = 'baz';

	public function fooBar(string $boo_bah) : string {
		$bar_baz = $boo_bah;

		return $this->foo_bar . $bar_baz;
	}
}
~~~


### 9. (new) DocBlocks

DocBlocks SHOULD always be defined for class definitions if relevant.

DocBlocks MUST always be defined for class fields and methods.

DocBlocks MAY be defined inline for variables.

[@see]: http://docs.phpdoc.org/references/phpdoc/tags/see.html
[@property]: http://docs.phpdoc.org/references/phpdoc/tags/property.html
[@property-read]: http://docs.phpdoc.org/references/phpdoc/tags/property-read.html
[@property-write]: http://docs.phpdoc.org/references/phpdoc/tags/property-write.html
[@method]: http://docs.phpdoc.org/references/phpdoc/tags/method.html
[@param]: http://docs.phpdoc.org/references/phpdoc/tags/param.html
[@return]: http://docs.phpdoc.org/references/phpdoc/tags/return.html
[@throws]: http://docs.phpdoc.org/references/phpdoc/tags/throws.html
[@deprecated]: http://docs.phpdoc.org/references/phpdoc/tags/deprecated.html


### 9.1. Class DocBlocks

Classes MUST have a DocBlock defined if it uses any magic properties or methods.

For classes it is important to put care into defining the available properties
and methods that is provided through the magic methods `__get()`, `__set()`
and `__call()`

- '[@see] \[URI | FQSEN] \[\<description>]' *- Use when referencing other code or websites*
- '[@property] \[Type] \[name] \[\<description>]' *- Define read-write property available through magic*
- '[@property-read] \[Type] \[\<description>]' *- Define read-only property available through magic*
- '[@property-write] \[Type] \[\<description>]' *- Define write-only property available through magic*
- '[@method] \[return type] \[name](\[\[type] \[parameter]<, …>]) \[\<description>]' *- Define method available through magic*
- '[@deprecated] \[<version>] \[\<description>]' *- Mark deprecated classes*


~~~php
<?php
namespace Vendor\Package;

/**
 * Optional description
 *
 * @property Foo $foo
 * @property-read array $bar
 * @property-write string $baz
 * @method Relation $relation
 */
class ClassName
{
	public function fooBar(string $boo_bah) : string {
		// method body
	}
}
~~~


### 9.2. Function DocBlocks

Functions and methods MUST have a DocBlock defined with detailed documentation
of the function signature.

DocBlocks for functions and methods SHOULD start with a relevant description
of the purpose of the function.

- '[@see] \[URI | FQSEN] \[\<description>]' *- Use when referencing other code or websites*
- '[@param] \[Type] \[name] \[\<description>]' *- Define function arguments*
- '[@return] \[Type] \[\<description>]' *- Define return types*
- '[@throws] \[Type] \[\<description>]' *- Define one or more possible exceptions*
- '[@deprecated] \[<version>] \[\<description>]' *- Mark deprecated methods*

~~~php
<?php
namespace Vendor\Package;

class ClassName
{
	/**
	 * Relevant description of the method.
	 *
	 * @param string $boo_bah
	 *
	 * @return string
	 */
	public function fooBar(string $boo_bah) : string {
		// method body
	}
}
~~~


### 9.3. Field DocBlocks

Class fields MUST have a DocBlock defined with detailed documentation
of the field type.

DocBlocks for fields SHOULD start with a relevant description
of the purpose of the field, but only if the field name isn't
sufficiently descriptive.

- '[@see] \[URI | FQSEN] \[\<description>]' *- Use when referencing other code or websites*
- '[@var] \[Type] \[$element_name] \[\<description>]' *- Define a variable type*
- '[@deprecated] \[<version>] \[\<description>]' *- Mark deprecated methods*

~~~php
<?php
namespace Vendor\Package;

class ClassName
{
	/**
	 * Relevant description of the field.
	 *
	 * @var string
	 */
	private $foo;

	public function fooBar(string $boo_bah) : string {
		// method body
	}
}
~~~


### 9.4. Inline variable DocBlocks

Variables MAY have a DocBlock defined to document the variable type.

DocBlocks for variables SHOULD be kept in a single line, defining both
the type and the variable name.
It MAY be multi line if a description should be necessary.

- '[@var] \[Type] \[$element_name] \[\<description>]' *- Define a variable type*

~~~php
<?php
namespace Vendor\Package;

class ClassName
{
	public function fooBar(string $boo_bah) : string {
		/** @var int $baz */
		$bar = 123;
	}
}
~~~


### 9.5. Arrays/Collections

DocBlocks for arrays MUST define the type of the array values if known.

Documenting collection classes MUST define both the collection class and
the type of the values.

~~~php
<?php
namespace Vendor\Package;

class ClassName
{
	/**
	 * @var string[]
	 */
	public $names;

	/**
	 * @var Collection|User[]
	 */
	public $users;
}
~~~


