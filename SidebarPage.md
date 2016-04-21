**reStText example**
<pre>
To test if number is<br>
positive [[pos]], use:<br>
``n > 0``. Now absolute<br>
function will be::</pre>```c

int abs(int n) {
if( [[=pos]] )
return n;
else return -n;
}
```
**Another: _placeholder and
multi-part_**
<pre>
Standard C headers guard<br>
[[hguard]] is::</pre>```c

#ifndef ${file}_H
#define ${file}_H```<pre>
and ``#endif`` at the end.<br>
So, [[file.x, prn.h]]::</pre>```c

[[=hguard.0, file:prn]]
#define PRN(x) puts(x)
[[=hguard.1]]```