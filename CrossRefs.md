# Introduction #

<img src='http://nano-lp.googlecode.com/files/refsfile.png' alt='Screenshot of reference file' width='90%' height='90%'>

<b>Fig, <i>screenshot of reference file since ver. 1.0h</i></b>
<br />

NOTE: <i>image above was grabbed from tests so files has extensions .out, instead of .c or .h (tests use .master, .out, then compares them)</i>

To generate cross-references file, run tool with <code>-r</code> command line option. This file has the same name as input file but with suffix <code>-refs</code> and extension <code>.html</code>. There will be saved all defined code chunks, cross-references, information about input and other.<br>
<br>
All commands there are links (cross-references). Commands pasted by glob-paths are accessible via popup-box (move mouse over such glob-paths) (at the moment it does not work in IE).<br>
<br>
Also will be created CSS style file with name <code>nanolp.css</code>, if not exists already in output directory (to avoid loosing of users CSS changes if they were done).