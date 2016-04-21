# What is the chunk #
Fragment of program source code

# What is the inline and block chunks #
**Inline** means ONE LINE. **Block** means several lines with CRLF symbols.

# Why is used inline chunk #
Because there are very small code fragments, may be one expression.

# What is the command #
Command means the same like Mr. D. Knuth _macros_. Command is used to:
  * give name to chunk to past it somewhere later
  * perform some actions (special commands: include another file, save to file...)

# How to define inline and block chunks #
It depends on used input format. For WiKi based, inline code is MONOSPACE/INLINE/MONOTYPED text fragments.

Block code is VERBATIM CODE BLOCK, SOURCE CODE FRAGMENT and depends on used input file format too.

In OpenOffice STYLE NAME is used (see [Notes](Notes.md)) to detect text fragments formatted in code style. In TeX - TeX-commands are used (all of these are configured via [ConfigFile](ConfigFile.md)).

# How to define command #
Command is the plain, usual text in your document. Np special formatting or styling. Only one exception: this fragment is surrounded by two special strings, for example: `[[some command]]` - here you are symbols `[[` and `]]`. These strings are configurable via [ConfigFile](ConfigFile.md).

# What should I write between surrounds symbols #
If you use special (built-in) command, you should to use it's convenient syntax. In other cases, you can use any text, BUT RIGHT PRACTICE is to use PATH instead of plain command name: `[[max_func]]` vs. `[[funcs.max]]`. Dot is used as slash delimiter in file systems paths.

# How to use defined command #
You can paste command in some code chunks. in this case PATH (name) of command should be prefixed with 'equals' symbol: `[[=funcs.max]]`.

# Can I use templating in chunks #
Yes. Instead of plain text, use string with dollar symbol prefix: `$some_variable`. But if there are special symbols in it's name: `${my var}`.
  * To substitute with it's value, point out value in command substitution: `[[=funcs.max, var:value of var]]`. See more in [Syntax](Syntax.md).
  * You can also use variables dictionaries with special command [use](SpecialCommands#use_command.md) (see also [paste](Syntax#Pasting.md) about it).
  * Also it is possible to wrap text with another chunks (multi-part commands).

# Can I include another LP program #
Sure. With special command [use](SpecialCommands#use_command.md).

# What about cyclic including #
Cycles are auto-detected and error message is raised in console.

# Can I paste several commands in the same time #
Yes. You can use globbing (see [Syntax](Syntax.md)) to select several commands (good is when their names are in dot-path-notation, like "a.b.c"), see: `[[=funcs.*]]`. Also you can set: variables' values, how to join chunks and other options.

# Can I use NanoLP on Web #
Yes. First, you can use LP programs from Web for tangling (extracting source codes from LP document) with URL instead of filename in `-i` command line option, also you can use URLs in `<<use>>` special command to import LP programs from Web sites. Also there is [Publish](Publish.md) facility: user can prepare HTML files for publishing on the Web. And sure HTML/XML parsing is supported.

# Is this tool Python 3 compatible #
Yes. It works with Python 2.7, Python 3+.