# Introduction #

It's very simple, has name 'lprc'. Lookup order of 'lprc' is:
  1. First, try folder of input file
  1. Then try current working directory
  1. And the script directory

Running with -h options shows real directory of 'lprc' file.

It has form:
```
PARAM = VALUE
...
```
Example of current version:
```
# Markdown file extensions
MDPARSER_EXT = .md, .mmd, .txt
# Markdown surround symbols
MDPARSER_SURR = [[, ]]

# OpenOffice file extensions
OOPARSER_EXT = .odt
# OpenOffice surround symbols
OOPARSER_SURR = [[, ]]
# OpenOffice code elements style name
OOPARSER_STYLE = lpcode

# Creole file extensions
CREOLEPARSER_EXT = .creole, .cre, .crl
# Creole surround symbols
CREOLEPARSER_SURR = @@, @@

# ReStructuredText file extensions
RSTPARSER_EXT = .rst, .rest, .restr
# ReStructuredText surround symbols
RSTPARSER_SURR = @@, @@
.......
```
Main parameters for any parser are PARSER\_EXT and PARSER\_SURR.

PARSER\_EXT binds file extensions for this parser.

PARSER\_SURR defines two strings as surround-symbols for any command. For example, if they are `[[` and `]]`, commands will use syntax: `[[COMMAND-TEXT]]`. What symbols to use depends on used document format (Markdown, Creole, etc.) and programming language in code-chunks. For example, `[[,]]` are safe for C, but not for Creole...