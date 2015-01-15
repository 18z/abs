第二章：從 Sha-bang (#!) 入門
---
In the simplest case, a script is nothing more than a list of system commands stored in a file.

>`若舉一最簡單的例子，所謂的腳本(script)就是一個由許多系統指令組合而成的單一檔案。`

At the very least, this saves the effort of retyping that particular sequence of commands each time it is invoked.

>`至少，在每次需使用一連串特定指令時，它讓使用者省了不少力氣。`

**Example 2-1. cleanup: A script to clean up log files in /var/log**

```bash
# Cleanup
# Run as root, of course.

cd /var/log
cat /dev/null > messages
cat /dev/null > wtmp
echo "Log files cleaned up."
```

There is nothing unusual here, only a set of commands that could just as easily have been invoked one by one from the command-line on the console or in a terminal window.

>`以上範例就如同平常在終端機中所使用的系統指令一樣，一行接著一行並沒有任何特別之處。`

The advantages of placing the commands in a script go far beyond not having to retype them time and again. 

>`將指令寫在腳本(script)中的優點在於它不必花費多餘的時間與力氣重複輸入同樣的指令。`

The script becomes a program -- a tool -- and it can easily be modified or customized for a particular application.

>`腳本(script)可以算是一支程式(program)抑或是一個工具(tool)，並且它能針對不同應用需求而輕易去做修改或客製化。`

**Example 2-2. cleanup: An improved clean-up script**

```bash
#!/bin/bash
# Proper header for a Bash script.

# Cleanup, version 2

# Run as root, of course.
# Insert code here to print error message and exit if not root.

LOG_DIR=/var/log
# Variables are better than hard-coded values.
cd $LOG_DIR

cat /dev/null > messages
cat /dev/null > wtmp


echo "Logs cleaned up."

exit #  The right and proper method of "exiting" from a script.
     #  A bare "exit" (no parameter) returns the exit status
     #+ of the preceding command. 
```

Now that's beginning to look like a real script. But we can go even farther . . .

>`現在這腳本越來越像樣了，但我們還可以再走遠一點點。`

**Example 2-3. cleanup: An enhanced and generalized version of above scripts.**

```bash
#!/bin/bash
# Cleanup, version 3

#  Warning:
#  -------
#  This script uses quite a number of features that will be explained
#+ later on.
#  By the time you've finished the first half of the book,
#+ there should be nothing mysterious about it.



LOG_DIR=/var/log
ROOT_UID=0     # Only users with $UID 0 have root privileges.
LINES=50       # Default number of lines saved.
E_XCD=86       # Can't change directory?
E_NOTROOT=87   # Non-root exit error.


# Run as root, of course.
if [ "$UID" -ne "$ROOT_UID" ]
then
  echo "Must be root to run this script."
  exit $E_NOTROOT
fi  

if [ -n "$1" ]
# Test whether command-line argument is present (non-empty).
then
  lines=$1
else  
  lines=$LINES # Default, if not specified on command-line.
fi  


#  Stephane Chazelas suggests the following,
#+ as a better way of checking command-line arguments,
#+ but this is still a bit advanced for this stage of the tutorial.
#
#    E_WRONGARGS=85  # Non-numerical argument (bad argument format).
#
#    case "$1" in
#    ""      ) lines=50;;
#    *[!0-9]*) echo "Usage: `basename $0` lines-to-cleanup";
#     exit $E_WRONGARGS;;
#    *       ) lines=$1;;
#    esac
#
#* Skip ahead to "Loops" chapter to decipher all this.


cd $LOG_DIR

if [ `pwd` != "$LOG_DIR" ]  # or   if [ "$PWD" != "$LOG_DIR" ]
                            # Not in /var/log?
then
  echo "Can't change to $LOG_DIR."
  exit $E_XCD
fi  # Doublecheck if in right directory before messing with log file.

# Far more efficient is:
#
# cd /var/log || {
#   echo "Cannot change to necessary directory." >&2
#   exit $E_XCD;
# }




tail -n $lines messages > mesg.temp # Save last section of message log file.
mv mesg.temp messages               # Rename it as system log file.


#  cat /dev/null > messages
#* No longer needed, as the above method is safer.

cat /dev/null > wtmp  #  ': > wtmp' and '> wtmp'  have the same effect.
echo "Log files cleaned up."
#  Note that there are other log files in /var/log not affected
#+ by this script.

exit 0
#  A zero return value from the script upon exit indicates success
#+ to the shell.
```

Since you may not wish to wipe out the entire system log, this version of the script keeps the last section of the message log intact. 

>`由於不希望消除整個系統紀錄，以上版本的腳本可以讓最新的系統紀錄保留。`

You will constantly discover ways of fine-tuning previously written scripts for increased effectiveness.

>`未來你會不斷發現提升舊腳本效率的方法。`

The sha-bang (	#!) [1] at the head of a script tells your system that this file is a set of commands to be fed to the command interpreter indicated. 

>`腳本開頭的 sha-bang (#!)是告訴系統此腳本由一組系統指令組成，並且需要由指令直譯器(command interpreter)解讀。`

The #! is actually a two-byte [2] magic number, a special marker that designates a file type, or in this case an executable shell script (type man magic for more details on this fascinating topic). 

>`#!實際上是兩個位元組[2]的魔術數字(magic number)，它是可以指明檔案類型的特殊標記，在上述範例中是標記檔案為可執行的腳本(你可以輸入 man 去了解更多有關這迷人主題的詳細資訊)。`

Immediately following the sha-bang is a path name. 

>`緊接在 sha-bang 後面的是路徑名稱`

This is the path to the program that interprets the commands in the script, whether it be a shell, a programming language, or a utility. 

>`這是解讀腳本內容的程式路徑，它可能是 shell、程式語言或者是應用程式。`

This command interpreter then executes the commands in the script, starting at the top (the line following the sha-bang line), and ignoring comments. [3]

>`指令直譯器(command interpreter)之後會從腳本第一行(接在 sha-bang 這行後面)開始執行系統指令，並且會忽略註解部分。`

```bash
#!/bin/sh
#!/bin/bash
#!/usr/bin/perl
#!/usr/bin/tcl
#!/bin/sed -f
#!/bin/awk -f
```

Each of the above script header lines calls a different command interpreter, be it /bin/sh, the default shell (bash in a Linux system) or otherwise. [4] 

>`以上每行腳本標頭代表呼叫不同的指令直譯器(command interpreter)，可以透過 /bin/sh (Linux 系統的 bash)或其他程式執行它[4]。`

Using #!/bin/sh, the default Bourne shell in most commercial variants of UNIX, makes the script portable to non-Linux machines, though you sacrifice Bash-specific features. 

>`#!/bin/sh 是最商業化 Unix 預設的 Bourne shell，使用它可以使腳本移植到非 Linux 系統，雖然必須犧牲部分 Bash 功能。`

The script will, however, conform to the POSIX [5] sh standard.

>`然而，這腳本將要符合 POSIX[5] sh 的標準。`

Note that the path given at the "sha-bang" must be correct, otherwise an error message -- usually "Command not found." -- will be the only result of running the script. [6]

>`要注意的是 sha-bang 後面所接的路徑必須是正確的，否則執行結果只會出現錯誤訊息，通常是 "Command not found."。[6]`

\#! can be omitted if the script consists only of a set of generic system commands, using no internal shell directives. 

>`如果腳本內容只是由一組系統指令所組成，並且沒有使用內置 shell 指令，則 \#! 可以省略。`

The second example, above, requires the initial #!, since the variable assignment line, lines=50, uses a shell-specific construct. [7] 

>`上述第二個範例一開始需要使用 #!，因為變數分配使用 shell 特定結構 lines=50。[7]`

Note again that #!/bin/sh invokes the default shell interpreter, which defaults to /bin/bash on a Linux machine.

>`再次注意，#!/bin/sh 會呼叫預設的 shell 直譯器，在 Linux 中的預設路徑為 /bin/bash。`


This tutorial encourages a modular approach to constructing a script. 

>`本教程鼓勵使用模組化的方法去建立腳本內容。`

Make note of and collect "boilerplate" code snippets that might be useful in future scripts. 

>`記下並蒐集“樣板”程式碼片段，這將有助於未來撰寫腳本。`

Eventually you will build quite an extensive library of nifty routines.

>`最終，你將會建立基本例行程序的函式庫(library)。`

As an example, the following script prolog tests whether the script has been invoked with the correct number of parameters.
<<<<<<< HEAD
=======

>`如同以下範例，範例中腳本首先測試是否以正確的參數個數呼叫腳本。`
>>>>>>> origin/master

```bash
E_WRONG_ARGS=85
script_parameters="-a -h -m -z"
#                  -a = all, -h = help, etc.

if [ $# -ne $Number_of_expected_args ]
then
  echo "Usage: `basename $0` $script_parameters"
  # `basename $0` is the script's filename.
  exit $E_WRONG_ARGS
fi
```

Many times, you will write a script that carries out one particular task. The first script in this chapter is an example. Later, it might occur to you to generalize the script to do other, similar tasks. Replacing the literal ("hard-wired") constants by variables is a step in that direction, as is replacing repetitive code blocks by functions.

**Notes**


[1]More commonly seen in the literature as she-bang or sh-bang. This derives from the concatenation of the tokens sharp (#) and bang (!).

[2]Some flavors of UNIX (those based on 4.2 BSD) allegedly take a four-byte magic number, requiring a blank after the ! -- #! /bin/sh. According to Sven Mascheck this is probably a myth.

[3]The #! line in a shell script will be the first thing the command interpreter (sh or bash) sees. Since this line begins with a #, it will be correctly interpreted as a comment when the command interpreter finally executes the script. The line has already served its purpose - calling the command interpreter.

If, in fact, the script includes an extra #! line, then bash will interpret it as a comment.
```bash
#!/bin/bash

echo "Part 1 of script."
a=1

#!/bin/bash
# This does *not* launch a new script.

echo "Part 2 of script."
echo $a  # Value of $a stays at 1.
```

[4]This allows some cute tricks.

```bash
#!/bin/rm
# Self-deleting script.

# Nothing much seems to happen when you run this... except that the file disappears.

WHATEVER=85

echo "This line will never print (betcha!)."

exit $WHATEVER  # Doesn't matter. The script will not exit here.
                # Try an echo $? after script termination.
                # You'll get a 0, not a 85.
```

Also, try starting a README file with a #!/bin/more, and making it executable. The result is a self-listing documentation file. (A here document using cat is possibly a better alternative -- see Example 19-3).

[5]Portable Operating System Interface, an attempt to standardize UNIX-like OSes. The POSIX specifications are listed on the Open Group site.

[6]To avoid this possibility, a script may begin with a #!/bin/env bash sha-bang line. This may be useful on UNIX machines where bash is not located in /bin

[7]If Bash is your default shell, then the #! isn't necessary at the beginning of a script.	However, if launching a script from a different shell, such as tcsh, then you will need the #!.
