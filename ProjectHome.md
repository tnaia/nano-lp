  * **NEW VERSION: 1.0!**
  * **PASSED ALL TEST ON LINUX, WINDOWS**
  * **ADDED PRESENTATION**

Ideal for [collaborative work and personal projects](AboutNanoLP#What_is_good_for.md).

Supported input formats:
  * OpenOffice/LibreOffice
  * MarkDown/MultiMarkdown
  * Creole
  * reStructuredText
  * TeX/LaTeX
  * txt2tags
  * Asciidoc
  * HTML/XML
  * ... and all based on their syntax!
**with clean, simple and readable [Syntax](Syntax.md)!**

Base functions:
  * [definition of command (macros) with placeholders in the body (code chunk)](Syntax#Command_syntax.md)
  * [variables dictionaries (for substitution of placeholders)](SpecialCommands#vars_command.md)
  * [pasting command code chunk with substitution of placeholders](Syntax#Pasting.md)
  * [definition of multiple parts code-chunks (for wrapping, etc.)](Syntax#Set_of_commands.md)
  * [joining, 'ending', etc. several code chunks](Syntax#Globbing.md)
  * ['globbing' commands when paste](Syntax#Globbing.md)
  * [including one file to another (library)](SpecialCommands#use_command.md)
  * [custom event handlers (filters in chain/pipe manner)](Events.md)
  * [supporting URLs in file names (read via HTTP)](FAQ#Can_I_use_NanoLP_on_Web.md)
  * [prepare of HTML files (with LP commands) for Web publishing](Publish.md)
  * [generating cross-references file](CrossRefs.md)
  * [auto-detection of cycles](FAQ#What_about_cyclic_including.md)
  * [configurable via simple .INI like file](ConfigFile.md)
  * [works with Python 2.7 - Python 3+](Notes#Features.md)
  * [works with Unicode (UTF8)](Notes#Features.md)
  * [extendible](Notes#Extending.md)
  * Custom surround symbols (different for doc and code)
  * Different code sources: local FS, ZIP, HTTP, FTP, shell

For more info see WIKI here.

For examples, see tests/ directory in archive. More about [test anatomy](Tests#Files_tests.md)