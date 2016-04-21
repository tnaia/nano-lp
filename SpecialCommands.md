# Introduction #

There are several special commands: `<<file.*>>`, `<<use>>`... To see all available, run tool with `-h` option.

## file command ##

It's used for saving it's chunk into file and has form:
```
  <<file.ANY-TEXT, FILE-NAME>> ... chunk ...
```

## use command ##

It's used to include another file into current (like library):
```
  <<use, FILE-NAME, mnt:MOUNT-POINT>>
```
and does not requires chunk. **Mount-point** is optional keyword argument and it's used to prefix all included chunks. If originally one have path `a.b` and **mnt** is `c.d`, so resulting path will be `c.d.a.b` (to avoid name conflicts).

All variable dictionaries of included file will be available in new paths (if **mnt** is used), so `$x` (from anonymous dictionary) becomes `$mnt.x`, and `$dict1.x` becames `$mnt.dict1.x`

## vars command ##

Creates dictionary of variables (placeholders in chunks), something like global variables in usual programming languages. There are 2 forms, first is anonymous dictionary, for ex.:
```
  <<vars, a:1, b:2>>
```
and named dictionary:
```
  <<vars, d, a:1, b:2>>>
```
So, placeholders are: `$a`, `$b`, and `${d.a}`, `${d.b}`. Explicitly set of arguments has higher priority, so:
```
  <<=some, a:1000>>
```
will use a = 1000. When file is included in another, all it's variables will be imported too (see about **use** command)

## on command ##

Setup event handler for one or more (with globbing) defined commands, for ex.:
```
<<on.Cmd, gpath:c.f1, do.define:upper chunktext>>
<<on.Cmd.define, gpath:c.f2, do:|lower chunktext>>
<<on.Cmd.paste, gpath:c.f4, do:|upper chunktext>>
```
Syntax is:
```
<<on.CLASS, gpath:GLOB, do.EVENT:HANDLER, do.EVENT:HANDLER...>>
  or
<<on.CLASS, gpath:GLOB, do:HANDLER>>
  or
<<on.CLASS.EVENT, gpath: GLOB, do:HANDLER>>
```
`CLASS` usually is Cmd (case has matter!) - name of Python-class to be matched. `GLOB` matches concrete commands. `EVENT` is some event name:
  * define -- happens when command is defining
  * paste -- happens when command is paste into another chunk
  * post -- happens after all file was processed
`HANDLER` binds callback function. There are two forms of `HANDLER`:
  * one argument: `FUNC FIELD-NAME`
  * all arguments: `FUNC`
All registered handlers are in `handlers.py` module. Symbol `'|'` (pipe) is used to setup order of **PIPING** (or **CHAINING**): when `'|'` is first - process event **after** previous, last - process event **before** previous handler, without - process **instead of** previous handler.

Also is possible to handle events of command where it's defining, see [Syntax](Syntax.md).

_DEVNOTE_:

  * handler signatures are:
```
  func(one_arg)
  func(sender_obj, **kw_args)
```
  * to break chaining mechanism, user-defined handler can raise StopChain exception.
  * all events can be found as methods in form `onEVENT(...)` of `CLASS`. For ex., `<<on.Cmd...>>` handles events for ondefine(), onpost(), onpaste() Cmd class methods.