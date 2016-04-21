# Introduction #

There is event handling mechanism. User can handle one or more events for concrete command or commands set to modify usual event-handling result.

There are 2 ways to do it:
  * in in-place manner
  * in global manner

See more about [in-place manner](Syntax#Event_handling.md) and [global manner](SpecialCommands#on_command.md).

DEVNOTES:
  * in-place handlers are **instance based** handlers
  * global handlers are **class based** handlers
  * class based handlers are created by `<<on.*>>` cmd: `<<on.CLASS.EVENT, do:...>>` or `<<on.CLASS, do.EVENT1:..., do.EVENT2:...>>`. Class based needs 'gpath' arg. necessary to match concrete instances!
  * instance based handlers are created in any user-command (i.e., macros) by `<<some, do.EVENT1:..., do.EVENT2:...>>`.

So, scheme of handling is:
```
recepient, event - matching -> do: onEVENT() + handlers
                         or -> do: __onEVENT__() only, if exists
```
`recepient` is macthed instance. `onEVENT()` is callback of successor, it should call `BaseClass.onEVENT()`