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
