# Fullrate Online Javascript Coding Style Guide

***-- Don't know how to descripe this yet --***

The intent of this guide is to reduce cognitive friction when scanning code
from different authors. It does so by enumerating a shared set of rules and
expectations about how to format Javascript code.

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be
interpreted as described in [RFC 2119].

[RFC 2119]: http://www.ietf.org/rfc/rfc2119.txt


## 1. Overview

- Will come as we go


## 2. Default naming

We have a few special/magic things around the codebase that would benefit
from using a standardized name to avoid any unnecessary confusion.
New additions or discovery of existing things should be added here as needed.

### 2.1. Comoso PageContent modules

Located in `public/js/comoso/pagecontent/*.js`

This magic argument MUST be named `CMS` and it will hold ... I don't know


```js
define(
	'pagecontent/module_name',
	['pd', 'jquery'],
	/**
	 * @param {module:pd} pd
	 * @param {module:jquery} $
	 */
	function (pd, $) {
		/**
		 * @param {Object} CMS - Someone write a short description of this, I'm not entierly sure about it xD
		 */
		return function (CMS) {
			return CMS;
		};
	}
);
```


### 2.2. Public PageContent modules

Located in `public/js/comoso/pagecontent/public/*.js`

This magic argument MUST be named `PAGECONTENT` and it will hold the variables
you defined when linking the stylesheet from your Page Content class.


```js
define(
	'pagecontent/public/module_name',
	['pd', 'jquery'],
	/**
	 * @param {module:pd} pd
	 * @param {module:jquery} $
	 */
	function (pd, $) {
		/**
		 * @param {Object} PAGECONTENT - The data passed when defining the script in the PageContent class
		 */
		return function (PAGECONTENT) {
			return PAGECONTENT;
		};
	}
);
```

In the following example, the `PAGECONTENT` would contain the values `id`, `foo` and `redirect_url`

```php
<?php
namespace App\Page\Content;

class Element extends Base
{
	// ...

	/**
	 * @param bool $cache
	 *
	 * @return array
	 */
	public function scripts($cache = FALSE) {
		return [
			'pagecontent/public/module_name.js' => [
				'id'           => $this->base_id,
				'foo'          => $this->foo,
				'redirect_url' => route('content'),
			],
		];
	}

	// ...
}
```



## 3. Module dependencies

When defining a requireJS module anywhere, you SHOULD write JSDoc for the
dependencies you request in the main function.

```js
define(
	'pagecontent/public/module_name',
	['pd', 'jquery', 'lib/debug', 'dot', 'lib/userstatus'],
	/**
	 * @param {module:pd} pd
	 * @param {module:jquery} $
	 * @param {module:lib/debug} debug
	 * @param {module:dot} dot
	 * @param {module:lib/userstatus} userstatus
	 */
	function (pd, $, debug, dot, userstatus) {
		/**
		 * @type {Object}
		 */
		return {
			foo: 'bar'
		};
	}
);
```
