第一章：Shell scripting
---

A working knowledge of shell scripting is essential to anyone wishing to become reasonably proficient 
at system administration, even if they do not anticipate ever having to actually write a script. 

對任何想管好系統的人來說，shell scriping 是必要的。

Consider that as a Linux machine boots up, it executes the shell scripts in /etc/rc.d 
to restore the system configuration and set up services.

Linux開機後，它會執行 /etc/rc.d 目錄下的shell scripts，藉以載入系統設定值以及啟動相關系統服務。

A detailed understanding of these startup scripts is important for analyzing the behavior of a system, 
and possibly modifying it.

若想分析或改變系統的行為，則對這些啟動 scripts 的了解是相當重要的。

The craft of scripting is not hard to master, since scripts can be built in bite-sized sections and there is only a fairly small set of shell-specific operators and options [1] to learn. 

寫腳本其實不難。因為腳本不必寫的很雜很長，且與其他程式語言比較，相對來說shell的運算子與options都較少，較好掌握。

The syntax is simple -- even austere -- similar to that of invoking and chaining together utilities at the command line, and there are only a few "rules" governing their use. 

Shell語法很簡單，甚至可用簡樸來形容。

Most short scripts work right the first time, and debugging even the longer ones is straightforward.

絕大多數簡短的腳本第一次執行時，就能顯示出正確結果。即使是較長的腳本在debugging上也相當的直覺。

In the early days of personal computing, the BASIC language enabled anyone reasonably computer proficient to write programs on an early generation of microcomputers. 

早期，只要對電腦精通的人，即能用BASIC語言在microcmomputers上面寫程式。
 
Decades later, the Bash scripting language enables anyone with a rudimentary knowledge of Linux or UNIX to do the same on modern machines.

幾十年後，任何對Linux或UNIX有一定了解的人，也能透過Bash腳本語言達成同樣的目的。

We now have miniaturized single-board computers with amazing capabilities, such as the Raspberry Pi.

現在我們有了像 Raspberry Pi這樣的小型裝置。

Bash scripting provides a way to explore the capabilities of these fascinating devices.

而Bash腳本提供了我們探索這些小型裝置capabilities的管道。

A shell script is a quick-and-dirty method of prototyping a complex application. 

Shell script對於建構一個複雜application的prototype來說，是一個快速又dirty的方法，在開發初期是相當好用的。

Getting even a limited subset of the functionality to work in a script is often a useful first stage in project development. 

In this way, the structure of the application can be tested and tinkered with, and the major pitfalls found before proceeding to the final coding in C, C++, Java, Perl, or Python.

也因如此，application的架構是可被測試與修補的，在用C, C++, Java, Perl 或Python 實作之前，也可能找到重大的bug。

Shell scripting hearkens back to the classic UNIX philosophy of breaking complex projects into simpler subtasks, of chaining together components and utilities. 

Shell scripting 也富有UNIX的哲學，即將許多複雜的projects分化成許多簡單的子項目，再將子項目串起來以達成projects的目的。

Many consider this a better, or at least more esthetically pleasing approach to problem solving than using one of the new generation of high-powered all-in-one languages, such as Perl, which attempt to be all things to all people, but at the cost of forcing you to alter your thinking processes to fit the tool.

許多人都將shell scripting視為是優雅的解決方案，而不選擇其他威力更強的語言，例如Perl。Perl嘗試達成所有人想達成的所有任務，但使用的成本就是它也強迫改變使用者的思路，如此才能將Perl用得淋漓盡致。

According to Herbert Mayer, "a useful language needs arrays, pointers, and a generic mechanism for building data structures." By these criteria, shell scripting falls somewhat short of being "useful." Or, perhaps not. . . .
