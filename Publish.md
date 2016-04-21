# Introduction #

NanoLP supports special processing of HTML files - preparing for Web publish. HTML files in this case are files with LP commands and uses surround symbols (as all other input formats), code chunks are placed into some HTML tags - all as usual, but preparing to publish means **modifying of input HTML file to be publish**:
  * adding link to nanolp-pub.css
  * adding link to nanolp-pub.js
  * embeed nanolp configuration Javascript
So, base idea of "publish" is to convert on the fly (on client-side of Web-browser) commands into clickable links.

# Details #

Preparing for publishing of one file is possible only once. Syntax is:
```
nlp.py -i some-lp.html -p URL
```
`URL` will be base address of all local links. It can be setup as:
```
-p URL
-p .
```
  1. If URL does not contain `protocol`, `http://` will be used.
  1. Last (only dot symbol) form means "use local links", so links will be `href="some-file"` instead of `href="URL/some-file"`.

Prepared HTML file content is the same, but added CSS and JS modifies it's content on client-side (in the user Web Browser) - it changes commands to links (glob-commands to popup-windows with links).

These HTML files can be published in Web sites, WiKis, etc. as online documentation BUT ALSO AS ONLINE LIBRARIES. So,
  * **user can extract (_tangle_) code from them**
  * or **uses them as libraries for own LP program**
**NOTE:** there is another way: place LP programs on some FTP/HTTP server and user can tangle or import as libraries these files by using full URLs in nlp.py tool (in `<<use>>` command or in command-line when he extracts sources). This way is more preferable, because HTML file usual is result of processing another input format and code-chunks can be presents in very different ways, not only in `<code>` or `<pre>` HTML-tags (so user should know these tags/style classes).

So main idea of publishing is:

**If LP program is in non-publishing format, user can convert it to HTML format, then prepares it for publishing on the Web**

# Files #

If 'nanolp-pub.css' and 'nanolp-pub.js' files does not exists, NanoLP creates them, otherwise they kept unmodified.