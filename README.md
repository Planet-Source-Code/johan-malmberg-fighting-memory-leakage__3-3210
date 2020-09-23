<div align="center">

## Fighting Memory Leakage


</div>

### Description

Memory leakage is probably one of the most difficult programming problems to solve. This article tell you why, and how to do it.
 
### More Info
 


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Johan Malmberg](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/johan-malmberg.md)
**Level**          |Intermediate
**User Rating**    |3.8 (30 globes from 8 users)
**Compatibility**  |C, C\+\+ \(general\), Microsoft Visual C\+\+, Borland C\+\+
**Category**       |[Debugging and Error Handling](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/debugging-and-error-handling__3-6.md)
**World**          |[C / C\+\+](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/c-c.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/johan-malmberg-fighting-memory-leakage__3-3210/archive/master.zip)





### Source Code

<br><font face="arial" size="2"><b>Fighting Memory Leakage</b><br><br>
<b>Errors and complex systems</b><br>
Any developer writing server applications, or other programs running continuously for a longer periods of time, knows how frustrating it can be with processes slowly allocating more and more memory until some other program finally crashes 3 days later after running out of memory. Memory leakage is probably one of the most difficult programming problems to solve, because you cannot easily search thousands of lines of code for a complex logical error that might cause a problem when some unlikely event occurs. If your application interacts with other programs as well, you might not even have any source code to search. If you are really unfortunate, a small error in your application could activate a buggy piece of code in some other program, and eventually that other program might crash the entire system after allocating all available memory. How are you supposed to find out what really happened?<br><br>
<b>Debugging and Testing</b><br>
Writing computer programs is not a simple matter. Computers can execute millions of instructions in one second, but they still don't know what to do if you tell them to "draw a circle". Fortunately you can easily make any computer draw a circle by combining a number of simpler instructions. By using even more instructions you can make the computer do even more impressive things, like drawing a house or decompressing a live video stream from a mars. The only problem is, the more instructions you add, the more likely you are to make an error. With modern programs consisting of thousands or millions of lines of code, errors are pretty much unavoidable. This wouldn't be a problem at all if there were only syntactic errors, since these are easily detected by the compiler, but there are also logical errors (bugs) that will pass right through your compiler without a single warning. Many errors are not even serious enough to cause any problems on their own, but when you combine a few of these errors, you get to spend hours reading your own code, trying to figure out what it really does. So how can we find the errors without spending to many hours on every line of code? The answer is pretty obvious. We run the program! If there are any bugs, they will probably show up after running the program for a while. Although this is a very efficient strategy, there are some errors that don't affect the user-interface or any other observable part of the program directly. These errors are much harder to find, since it may take hours or even days before they have any effects on the user-interface. To find these errors without spending hours or days on each test-update cycle, we need to keep track of some more abstract properties of the program, like memory and cpu-usage. By monitoring these properties for some time, you will be able to find trends and predict problems long before you actually get an error message.<br><br>
<b>Using WinTasks to inspect memory usage</b><br>
WinTasks 4 Professional from LIUtilities is a tool for inspecting running processes. On a Windows 2000/NT/XP system. It allows you to log the cpu and memory usage of each process continuously for many hours. Using this tool it is possible to find out which processes are leaking memory by examining the memory usage over the last few hours. Even if the errors causing the memory leakage are to small to cause any serious problems by themselves, the accumulated effect after running the program for many hours could be devastating. Without directly measuring memory usage, you probably won't find out until it's too late. Using WinTasks you will always have memory usage statistics available when needed. (WinTasks runs in the background constantly monitoring all processes) In this example I will try to show you how to use WinTasks 4 Professional to detect a memory leakage hours before it causes a more serious error. The following, very simple piece of code, was executed:<br>
while(true)<br>
{<br>
new char[1000000];<br>
Sleep(100);<br>
}<br>
When opening the memory and cpu statistics window in WinTasks, after running the program for a few minutes, this is what we see:<br><br>
<img src="http://www.liutilities.com/products/wintaskspro/graphics/memleak.gif"><br><br>
As you can see, the process "Form1" (green) is clearly using more and more memory. Even though the process has only been running for about 5 minutes, we can already see that Form1 is allocating approximately 1.5 percent of the memory per minute, which means it will probably crash or cause a serious problem in after another 30 minutes when memory usage reaches over 50% (depending on the system you are using). Without logging the memory usage, we would not know this until the program really crashed, but by looking at the memory usage graphs we can predict the problem in advance for any process. Now, imagine a program that drops less than one percent of memory per hour. It might take several days before you notice any abnormal behavior, but by using the technique described here, you could find out in maybe 20 minutes. This would shorten your test-update cycle by more than a hundred times, resulting in a shorter overall development times. Even though this technique may not by useful in every possible situation, if you are developing server applications or other software's intended to run continuously for longer periods of time, it is surely worth trying.
<br><br>Written by Emil Malmberg, Senior Software Developer for LIUtilities ( <a href="http://www.liutilities.com"> www.liutilities.com</a> )</font>

