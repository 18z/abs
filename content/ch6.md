Chapter 6. Exit and Exit Status

第六章：退出及退出狀態
---

The exit command terminates a script, just as in a C program. 

>`exit 指令可以讓腳本停止執行，觀念跟 C 語言接近。`

It can also return a value, which is available to the script's parent process.

>`exit 指令也可回傳一個值給該腳本的父程序。`

Every command returns an exit status (sometimes referred to as a return status or exit code).

>`每一個指令都會回傳一個 exit 狀態 (status)，有時也被稱為回傳狀態（return status） 或退出代碼（exit code）`

A successful command returns a 0, while an unsuccessful one returns a non-zero value that usually can be interpreted as an error code. 

>`一指令若被成功執行則回傳 0 值，若執行失敗，則回傳一個非 0 值。`

Well-behaved UNIX commands, programs, and utilities return a 0 exit code upon successful completion, though there are some exceptions.

>`一般而言，UNIX 指令、programs 或 utilities 在成功執行完畢後，會回傳 0 值。然而，在幾個情況下有特例。`

Likewise, functions within a script and the script itself return an exit status. 

>`同樣的，腳本內的函式及腳本本身執行結束後都會有一個回傳值。`

The last command executed in the function or script determines the exit status. 

>`函式或腳本內的最後一個指令將決定回傳值是多少。`

Within a script, an exit nnn command may be used to deliver an nnn exit status to the shell (nnn must be an integer in the 0 - 255 range).

>`在腳本中，指令 "exit nnn" (nnn 必須是介於0~255間的數字) 可被用來向 shell 傳遞 exit status。`

When a script ends with an exit that has no parameter, the exit status of the script is the exit status of the last command executed in the script (previous to the exit).

>`若一腳本 exit 時，沒有指定 exit status，則 exit status 就會是腳本內的最後一個被執行的指令。`

```bash
#!/bin/bash

COMMAND_1

. . .

COMMAND_LAST

# Will exit with status of last command.
# 回傳最後一個被執行指令的狀態。

exit
```

The equivalent of a bare exit is exit $? or even just omitting the exit.
exit $? 與直接省略 exit，皆與上面「只有一個exit」的結果相同。

```bash
#!/bin/bash

COMMAND_1

. . .

COMMAND_LAST

# Will exit with status of last command.
# 回傳最後一個被執行指令的狀態。

exit $?
```
```bash
#!/bin/bash

COMMAND1

. . . 

COMMAND_LAST

# Will exit with status of last command.
# 回傳最後一個被執行指令的狀態。
```

$? reads the exit status of the last command executed. 

>`$? 會讀取最後一個被執行指令的狀態。`

After a function returns, $? gives the exit status of the last command executed in the function. 

>`每當一個函式回傳訊息或參數值時，$? 就會給予函式中最後一個被執行指令的狀態。`

This is Bash's way of giving functions a "return value." [1]

>`這就是 Bash 函式「回傳值」的方式。 [1]`

Following the execution of a pipe, a $? gives the exit status of the last command executed.

>`若以 pipe 串接多指令，則 $? 回傳最後被執行指令的狀態。`

After a script terminates, a $? from the command-line gives the exit status of the script, that is, the last command executed in the script, which is, by convention, 0 on success or an integer in the range 1 - 255 on error.

>`當一腳本終止時，$? 就會反應出最後被執行指令的狀態，0 表示被成功執行、1-255 之間的數值則表示執行時各種可能的錯誤發生。`

Example 6-1. exit / exit status

>`範例 6-1. 退出/退出狀態`

```bash
#!/bin/bash

echo hello
echo $?    # Exit status 0 returned because command executed successfully.
           # 指令執行成功，回傳退出狀態值 0。

lskdf      # Unrecognized command.
           # 無法辨識的指令。
echo $?    # Non-zero exit status returned -- command failed to execute.
           # 回傳非 0 數值 -- 指令執行失敗。

echo

exit 113   # Will return 113 to shell.
           # 回傳 133 給 shell。
           # To verify this, type "echo $?" after script terminates.
           # 腳本執行完畢，輸入 echo $? 即可驗證是否為 113。

#  By convention, an 'exit 0' indicates success,
#+ while a non-zero exit value means an error or anomalous condition.
#  依慣例，exit 0 表示指令成功執行，若有非零值則表示異常狀況出現。

#  See the "Exit Codes With Special Meanings" appendix.
#  退出值與其意涵，請參考附錄 (Exit Codes With Special Meanings)
```

$? is especially useful for testing the result of a command in a script (see Example 16-35 and Example 16-20).

>`$? 在測試腳本中指令執行結果上，是相當好用的。(詳見 範例 16-35 及 16-20)`

The !, the logical not qualifier, reverses the outcome of a test or command, and this affects its exit status.

Example 6-2. Negating a condition using !

```bash
true    # The "true" builtin.
echo "exit status of \"true\" = $?"     # 0

! true
echo "exit status of \"! true\" = $?"   # 1
# Note that the "!" needs a space between it and the command.
#    !true   leads to a "command not found" error
#
# The '!' operator prefixing a command invokes the Bash history mechanism.

true
!true
# No error this time, but no negation either.
# It just repeats the previous command (true).


# =========================================================== #
# Preceding a _pipe_ with ! inverts the exit status returned.
ls | bogus_command     # bash: bogus_command: command not found
echo $?                # 127

! ls | bogus_command   # bash: bogus_command: command not found
echo $?                # 0
# Note that the ! does not change the execution of the pipe.
# Only the exit status changes.
# =========================================================== #

# Thanks, Stéphane Chazelas and Kristopher Newsome.
```

Certain exit status codes have reserved meanings and should not be user-specified in a script.

Notes

[1]	In those instances when there is no return terminating the function.
