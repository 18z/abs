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

根據 Herbert Mayer所說：「任一種useful的程式語言都需要陣列、指標以及generic mechanism來建立資料結構。」若依據上述標準，shell scripting好像就不那麼useful，甚至是不useful。

When not to use shell scripts

何時不適合用 shell scripts?

Resource-intensive tasks, especially where speed is a factor (sorting, hashing, recursion [2] ...)

需耗費大量運算資源的任務，尤其當執行速度是一重要因素時(例如：排序、hashing或遞迴等。)

Procedures involving heavy-duty math operations, especially floating point arithmetic, arbitrary precision calculations, or complex numbers (use C++ or FORTRAN instead)

需要大量數學運算，特別是浮點數運算、高精度計算或複數等(use C++ or FORTRAN instead)。

Cross-platform portability required (use C or Java instead)

有跨平台需求時不適用(use C or Java instead)

Complex applications, where structured programming is a necessity (type-checking of variables, function prototypes, etc.)

開發複雜的應用程式，特別是需要結構化編程時(type-checking of variables, function prototypes, etc.)

Mission-critical applications upon which you are betting the future of the company.

負有重大使命的應用程式。未來公司成功與否將賭在這個應用程式上。

Situations where security is important, where you need to guarantee the integrity of your system and protect against intrusion, cracking, and vandalism.

當安全議題是重要的時候，不適合用shell scripting。當你需確保系統安全並保護系統免於被入侵、破解及被破壞時。

Project consists of subcomponents with interlocking dependencies.

當project內的子元間彼此環環相扣時，不適用shell scripting。

Extensive file operations required (Bash is limited to serial file access, and that only in a particularly clumsy and inefficient line-by-line fashion.)

需對大量檔案做處理時。(Bash在處理檔案時，只能用笨拙且無效率的方式，一行一行讀取文件。)

Need native support for multi-dimensional arrays

需要使用到多維陣列時 (native support)

Need data structures, such as linked lists or trees

需要使用到資料結構方法，例如鏈結串列或樹。

Need to generate / manipulate graphics or GUIs

需要產生或操控圖形化介面時。

Need direct access to system hardware or external peripherals

需要直接操控硬體或外部連接設備。

Need port or socket I/O

需要使用到port或 socket I/O

Need to use libraries or interface with legacy code

需要使用到legacy code的libraries或interface。

Proprietary, closed-source applications (Shell scripts put the source code right out in the open for all the world to see.)

專有或封閉原始碼的應用程式 (shell scripts的內容是任何人都可看見的)

If any of the above applies, consider a more powerful scripting language -- perhaps Perl, Tcl, Python, Ruby -- or possibly a compiled language such as C, C++, or Java. Even then, prototyping the application as a shell script might still be a useful development step.

若遇到上述提到的情境，建議考慮使用更強大的腳本語言 -- 例如：Perl, Tcl, Python, Ruby 或者是 C, C++, Java。即使如此，使用shell script來建立應用程式的prototype也還是一個相當好用的方法。
