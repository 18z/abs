Chapter 5. Quoting

第五章：引號使用
===

Quoting means just that, bracketing a string in quotes.

>`引號包住的意思，就是用引號括住一段字串。`

This has the effect of protecting special characters in the string from reinterpretation or expansion by the shell or shell script.

>`這有保護字串中的特殊字元之效果，使其不被 shell 或腳本多做額外的解讀或展開。`

(A character is "special" if it has an interpretation other than its literal meaning.

>`(若一個字元可以有別於字面上的原意之解讀，則稱此字元為 "特殊字元"。`

For example, the asterisk * represents a *wild card* character in globbing and Regular Expressions).

>`例如，星號 * 在 globbing (如同後述範例) 與正規表示式裡有代表 "萬用字元" 的涵義)。`

```bash
bash$ ls -l [Vv]*
-rw-rw-r--    1 bozo bozo     324 Apr 2  15:05 VIEWDATA.BAT
-rw-rw-r--    1 bozo bozo     507 May 4  14:25 vartrace.sh
-rw-rw-r--    1 bozo bozo     539 Apr 14 17:11 viewdata.sh

bash$ ls -l '[Vv]*'
ls: [Vv]*: No such file or directory
```

In everyday speech or writing, when we "quote" a phrase, we set it apart and give it special meaning.

>`在日常談話與書寫中，當我們用 "引號包住" 一段片語時，它將與眾不同，並賦予特殊意義。`

In a Bash script, when we *quote* a string, we set it apart and protect its *literal* meaning.

>`在一個 Bash 腳本中，當我們用 "引號包住" 一段字串時，它將與眾不同，並保護它字面上的原意。`

Certain programs and utilities reinterpret or expand special characters in a quoted string.

>`某些程式與工具會針對被引號包住的字串裡的特殊字元多做額外的解讀或展開。`

An important use of quoting is protecting a command-line parameter from the shell, but still letting the calling program expand it.

>`引號的一個很重要的用途就是保護命令列參數免於被 shell 多做解讀，但仍有可能被呼叫的程式展開。`

```bash
bash$ grep '[Ff]irst' *.txt
file1.txt:This is the first line of file1.txt.
file2.txt:This is the First line of file2.txt.
```

Note that the unquoted `grep [Ff]irst *.txt` works under the Bash shell. [29]

>`注意：沒有引號包住的 "grep [Ff]irst *.txt" 在 Bash shell 底下仍可正常動作。[29]`

Quoting can also suppress echo's "appetite" for newlines.

>`引號包住還可以用來解除 echo 指令總是把 newlines (換行字元) 消化掉的行為。`

```bash
bash$ echo $(ls -l)
total 8 -rw-rw-r-- 1 bo bo 13 Aug 21 12:57 t.sh -rw-rw-r-- 1 bo bo 78 Aug 21 12:57 u.sh

bash$ echo "$(ls -l)"
total 8
-rw-rw-r--   1 bo bo   13 Aug 21 12:57 t.sh
-rw-rw-r--   1 bo bo   78 Aug 21 12:57 u.sh
```
