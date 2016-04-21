# Why yet another LP tool? #

Most of LP tools are old or out-of-date and uses special input file format with weird syntax. LP programs looks like crypto-text. This new tool has goals:
  * no special input file format, only already existed
  * simple syntax to keep code sources clean

# Main idea #

Main idea is to avoid processing document (LP source) format: no special format for input files, they can be Markdown, Creole, OpenOffice, etc...

<img src='http://nano-lp.googlecode.com/files/workflow.png' alt='Workflow schemes' width='60%' height='60%'>

So, this kind of LP tool knows about LP input format only how to extract LP commands and code chunks - <b>tangle</b>, weaving is not needed, input format is ready for <b>printing</b>, <b>publishing</b>, <b>reading</b>, etc.<br>
<br>
<h1>What is good for</h1>

NanoLP does not force you to use weird syntax for LP programs and its text formatting - you can use OpenOffice/LibreOffice suite even! It's ideal <b>for collaborating team members</b> to create <u>common code base, published in Intranet/Internet, always ready for code extraction or using as libraries, also reading or printing</u>. It's good for <b>personal usage</b> also due to <u>small size</u> and support of many <u>lightweight markups</u>.<br>
<br>
<h1>LP code anatomy</h1>

Nanolp detects next sequences:<br>
<pre><code>  ... command ... chunk ...<br>
</code></pre>
This means: <b>define named code chunk by this command</b>, or another, <b>link this command with this code chunk</b>
<pre><code>  ... command ... command ...<br>
</code></pre>
This means: <b>define named code chunk with empty body</b>, or <b>links this command with empty chunk</b> - <i>usually is used with special commands, not name some chunk, but to perform some actions (but special command may have chunk too)</i>.<br>
<pre><code>  ... command  ... chunk ... chunk ...<br>
</code></pre>
This means: <b>define named code chunks, each name is like original command but with numerical suffixes: .0, .1, .2, etc.</b> (see more about <a href='Syntax.md'>Syntax</a>).<br>
<br>
So, there are only rules:<br>
<ul><li>Nanolp detects monospace as inline (one line) code chunk<br>
</li><li>Nanolp detects code blocks as... code block chunk :)<br>
</li><li>Nanolp detects command as name of followed chunk/chunks (or as a special instruction, see <a href='SpecialCommands.md'>SpecialCommands</a>)</li></ul>

Nothing else! So, IDEA is too KEEP LP simple as it's possible and to use favorite document formats/document processors with only one extension: <b>special syntax for command</b>.<br>
<br>
<h1>Why so strange name?</h1>

<i>Nano</i> here means very small and simple.