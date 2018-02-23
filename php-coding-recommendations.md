# Fullrate Online PHP Coding Recommendations

This is a collection of recommendations we have agreed on and will help each
other to follow through our code review process.

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be
interpreted as described in [RFC 2119].

[RFC 2119]: http://www.ietf.org/rfc/rfc2119.txt


## 1. Overview

- We SHOULD do everything code related in English.

- We SHOULD avoid writing comments (except for [DocBlocks]).

- In security matters we MUST code as defensively as practically possible.


### 2. Language

We SHOULD do everything code related in English. This will reduce the
cognitive load by not having to switch language too often.

This includes, but is not limited to:

- Folder structure
- Classes
- Functions
- Variables
- Comments
- Commit messages

However, since our customer facing language is Danish, we MAY include
Danish words in comments when it will make more sense, and be more
readable than translating the words.


### 3. Comments

We SHOULD avoid writing comments (except for [DocBlocks]).
But we MUST write comments when the intent cannot be expressed
in another way. If a comment is needed, then write in proper
English and write a good description even a new person to the codebase
would understand.

#### Checklist:

| Question | Action |
|---|---|
| **Is this comment describing what the function is doing?** | Then that in the DocBlock for the function. |
| **Is this comment describing what the function returning?** | Then that in the DocBlock for the function. |
| **Can I do a simple refactor (rename variable, rename function, change order) in the code to make this comment obsolete?** | Then do that. |
| **Can I extract some logic to a new function with a name that makes the comment obsolete?** | Think about it, then do the refactor if it makes sense. |
| **Can I extract some logic to a new class that makes the comment obsolete?** | Think about it, then do the refactor if it makes sense. |

[DocBlocks]: php-coding-style-guide.md#9-new-docblocks


### 4. Security

In security matters we MUST code as defensively as practically possible.
Start out with everything locked down, and open for the things you need.


### 4.1. Security in Blade templates

Default to escaping all outputs using the double brackets `{{ $var }}`.

When the content can not be escaped, make sure the data is safe.
And if the content is coming fully or partially from any outside source,
make sure it is impossible to generate anything that could cause any
unexpected behaviour on the site.

When the data is secured output it unescaped using the
bracket bang bang `{!! $var !!}`.
