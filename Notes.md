# Implementation #

First version is developed in Python and is compatible with Python 2.7.x and Python 3.x, without any dependencies.

# Usage #

See command line syntax help:
```
  $ nlp.py -h
```
this also **shows available input formats**.

# Installation #

Standard Pythonic-way:
```
  $ python setup.py bdist
  $ python setup.py install
```

# Testing #

To run docstring tests, do:
```
  $ cd DIR-OF-PACKAGE
  $ python -m unittest discover test/
```
To run parsing/publishing/etc. (files) tests, do:
```
  $ cd DIR-OF-PACKAGE
  $ python -m unittest discover test/tests
```
See also [Tests](Tests.md).

# Features #

  * Works with Python 2.7 - Python 3.x.
  * Used charset for all input formats is UTF8.

# Extending #

To add new format support, extend base class Parser (see OOParser...).
To add new command processor, extend base class Cmd (see FileCmd...).
To add new event handler, define new handler (see lower()...).
See files:
  * commands.py -- registered commands
  * handlers.py -- registered event handlers
  * parsers.py -- registered parsers

# Special notes on input formats #

## OpenOffice ##

**Don't break line in inline code-chunks**, because parts will joined without spaces!

OOPARSER\_STYLE in ConfigFile is the name of **symbol** or **paragraph** style of **inline** or **block** code chunk. So, if you prefer to use another name in your LibreOffice documents, change its value in ConfigFile.

**Styles inheritance** are supported (OpenOffice inherits styles behind the scene often), **special symbols** and **direct formatting** are also supported (see test6/ for example).

## TeX ##

Parser detects forms as `\verb#some text#` as inline chunk. Instead of `verb` any word is possible (set it in TEXPARSER\_INLCMDS parameter in ConfigFile). There are, for example, `verb` and `verb*`. So, as inline are interpreters next forms:
```
  \verb#aaaaaaa#
  \verb{aaaaaaa}
  \verb*!aaaaaaa!
```
and so on...

Parser detects next forms as block chunks:
```
  \begin{verbatim}
  code text
  \end{verbatim}
```
OR
```
  \begin[some options]{verbatim}
  code text
  \end{verbatim}
```
Instead of `verbatim` any word of TEXPARSER\_BLKCMDS from ConfigFile are possible.

## txt2tags ##

Processes chunks:
```
  ``inline chunk``
```
as inline chunk.

```
  ``` one line chunk
```
as ONE LINE block chunk.

```
  ```
  ...code...
  ```
```
as usual block chunk.

## Asciidoc ##

**BASE IMPLEMENTATION**

Processes monospace fragments (`+some text+`) as inline chunks. Supported block chunks looks:
```
  [source]
  ----
  ...code...
  ----
```
OR
```
  [source, some_options]
  --------
  ...code...
  --------
```
OR
```
  <empty line>
  ----
  ...code...
  ----
```
Delimiter liens should has 4 or more '-' symbols.

## HTML/XML ##

There are a special setup parameters in ConfigFile:
```
...
# HTML code elements style names
HTMLPARSER_STYLES = lpcode
# HTML code elements tags
HTMLPARSER_TAGS = pre, code
# ignore errors types
HTMLPARSER_IGNORE = error, fatal
...
```
Code chunks are detected by tag names and/or class names (use one or both, if value is empty - this criteria is not used).

Parameter HTMLPARSER\_IGNORE is used to ignore some kinds of errors in invalid HTML files and can be `error, fatal, warning`.