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

Likewise, functions within a script and the script itself return an exit status. The last command executed in the function or script determines the exit status. Within a script, an exit nnn command may be used to deliver an nnn exit status to the shell (nnn must be an integer in the 0 - 255 range).
