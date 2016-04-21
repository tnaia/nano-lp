# Introduction #

Input files can be in supported format (Markdown, OpenOffice, Creole, etc.) and should content in it's document body sequence of **commands** and **code chunks**. Nano-LP extract stream of:
  * commands (macros in Dr. D. Knuth terminology)
  * inline code chunks
  * block code chunks
and interprets them.

General sequence is:
```
  ... command ... chunk ... command ... chunk
```
**...** means any text. **command** usually is the name of chunk. **chunk** may be inline or block (if input format distinguish inline and block code).

Also there are two aditional forms. First form:
```
  ... command ... command ...
```
creates commands with empty linked code chunk. And:
```
  ... command ... chunkA ... chunkB ...
```
creates command set (or command family), something like (commandA, chunkA), (commandB, chunkB).

# Command syntax #

Commands has two forms:
  * definition
  * pasting (in some code chunk)

In the both forms command looks:
```
  left-surrounder command-text right-surrounder
```
for ex.,:
  * definition: `<<some_cmd>>`
  * pasting: `<<=some_cmd>>`
**Surrounds** are configurable via ConfigFile and usually are different for differents input formats (usual they are `[[ and ]]`, or `<< and >>`, even `@@ and @@` - any strings).

**command-text** is:
```
  path, positional-args, keyword-args
```
**path** is the name of command and may consists of joined with dot (.) strings, like `funcs.openFile`. **path** may be long - text fragment, sentence (until first `','`), like:
<pre>
<<open all selected files>><br>
</pre>
All other parts of **command-text** may be omitted. Example of the full form is: `<<some_cmd, p1, p2, k1:a, k2:b>>`. Here are **positional-args**: p1, p2; **keyword-args**: k1, k2 with values _a_, _b_. Usually args are used in pasting of commands but there are exceptions.

Argument values can use escaping with backslash `\`:
```
  <<some_cmd, some_opt:\,>>
```
some\_opt has value `,`

# Pasting #

**Keyword-args** are used to replace placeholders in code chunks, for ex., chunk can be:
```
  if ($var > 0) print("Positive!")
```
and you can use pasting forms: `<<=cmd, var:x>>` to expand into:
```
  if (x > 0) print("Positive!")
```
or even: `<<=cmd, *:*>>` to expand (all placeholders in this case) into:
```
  if (var > 0) print("Positive!");
```

Also is possible to create variables dictionary; anonymous dictionary ex.:
```
    <<vars, v1:1, v2:2>>
```
or
```
    <<vars, dict1, v1:1, v2:2>>
```
Now anywhere in chunks will be allowed variables:
```
    $v1, $v2, ${dict1.v1}, ${dict1.v2}
```
Also it's possible to set what dictionary to use when substitute chunk:
```
    <<=some, *:$dict1>>
```
or even what variable value from another dictionary:
```
    <<=some, v:$dict1.v1>>
```

# Set of commands #

Looks like multi-part command. Each command has numerical suffix at the end of it's path, like: 0, 1, 2... And is accessible with this new path. Multi-part command is usable when programer needs to wrap some content. For ex. (in reStructuredText format):
```
  C language standard header file guarding <<hguard>> - is the famous trick::

    #ifndef ${file}_H
    #define ${file}_H

  and includes also last (at the bottom of H-file) line::

    #endif
```
and programmer can use it:
```
  <<=hguard.0, file:util>>
  ...
  <<=hguard.1>>
```

# Globbing #

So, each command usually has multi-component path (like in Tcl, or any file-system but instead of slash, dot is used). And programmer can use 'star'-symbol as glob-symbol to select (for paste) not one, but several commands. How it's pasting? Programmer can select way of this with keyword args **join**, **start**, **end**:
  * join - text fragment between each chunk
  * end - text fragment after each line
  * start - text fragment before each line
It's usuable when you paste several similar chunks. For ex.:
```
  <<=path.*, join:\n, end:;>>
```
produces something like:
```
  aaa;
  bbb;
  ...
```
User can use it in scenario (in some .h file) like:
```
  <<=all_declarations.*, join:\n, end:;>>
```

# Event handling #

There is mechanism of handling some internal events which can be used in chaining (or paping in Unix terminology) manner. For example, command events are supported:
  * define
  * post (post-processing after all file parsing is done)
  * paste (when command is paste into some chunk)
User can use one of pre-defined handlers or to define own (in Python), see [Extending](Notes#Extending.md). There are handlers:
  * lower
  * lstrip
  * rstrip
  * strip
  * swapcase
  * title
  * upper
  * etc.
used to handle one named parameter of event. Examples:
```
<<c.f3, do.define:|title chunktext>>
  or
<<c.f5, do.paste:title chunktext>>
```
here `define`, `paste` are names of event, `title` - is the name of handler-function, `chunktext` is the name of parameter. For this example, `title()` will 'titleize' all words: "aa bb cc" becames "Aa Bb Cc". Instead of modifying one parameter, it's possible to modify all, in this case syntax is:
```
<<CMD, do.EVENT:FUNC>>
```
but `FUNC` should has signatures of Python function: `func(sender_obj, **kw_args)`. Also user can handle several events in form:
```
<<CMD, do.EVENT1:HANDLER1, do.EVENT2:HANDLER2...>>
```

Symbol `'|'` setups order of piping: before previous handler, after, of instead.

_Also it's possible to use global handler (for commands' set) - see [ON command](SpecialCommands#on_command.md)_