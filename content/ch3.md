Chapter 3. Special Characters

第三章 特殊字元
---
What makes a character special? If it has a meaning beyond its literal meaning, a meta-meaning, then we refer to it as a special character. Along with commands and keywords, special characters are building blocks of Bash scripts.

>`是什麼讓字元特殊呢？假設他擁有超出其字面意義的意思，一個精粹的意思，那麼我們將它作為一個特殊字元。與其他命令與關鍵字詞被建築在Bash腳本之中。`

Special Characters Found In Scripts and Elsewhere

>`特殊字元可以在腳本或是其它地方中被發現`

Comments. Lines beginning with a (with the exception of ) are comments and will not be executed.

>`註解。句子開頭加上符號（如例子所示的『#』），代表這句子是註解並不會被執行。`

	# This line is a comment.</pre></code>

Comments may also occur following the end of a command.

>`註解也會出現在命令句的後方。`

```bash
	echo "A comment will follow." # Comment here.
	#                            ^ Note whitespace before #
```

Comments may also follow whitespace at the beginning of a line.

>`註解的符號後方也可以先接上空白再開始整個句子。`

```bash
	# A tab precedes this comment.
```	

Comments may even be embedded within a pipe.

>`註解甚至也可以在斜線中插入。`

```bash
	initial=( `cat "$startfile" | sed -e '/#/d' | tr -d '\n' |\
 	# Delete lines containing '#' comment character.
        	   sed -e 's/\./\. /g' -e 's/_/_ /g'` )
 	# Excerpted from life.sh scriptt
```

A command may not follow a comment on the same line. There is no method of terminating the comment, in order for "live code" to begin on the same line. Use a new line for the next command.

>`命令句不會跟在註解符號後。沒有任何方法可以將一句話中的註解給取消掉，為了讓新的句子能夠執行，使用新的一行作為新的命令。`
	
Of course, a quoted or an escaped # in an echo statement does not begin a comment. Likewise, a # appears in certain parameter-substitution constructs and in numerical constant expressions.

>`當然，在引用句或是echo中的『#』並不會開始一個全新的註解句。通常一個句子中的『#』代表某些參數結構式或是某些數據常量代表式。`

```bash
	echo "The # here does not begin a comment."
	echo 'The # here does not begin a comment.'
	echo The \# here does not begin a comment.
	echo The # here begins a comment.

	echo ${PATH#*:}       # Parameter substitution, not a comment.
	echo $(( 2#101011 ))  # Base conversion, not a comment.
	#Thanks, S.C.</pre></code>
	The standard quoting and escape characters (" ' \) escape the #.
```

>`透過基礎的引用和跳脫符號來消除『#』本身的註解意義。`

Certain pattern matching operations also use the #.

>`特定的匹配操作也會使用『#』。`

Command separator [semicolon]. Permits putting two or more commands on the same line.

>`命令分隔符號『;』。透過此符號能夠允許在同一列文字上放上兩個或是更多的命令。`

```bash
	echo hello; echo there

	if [ -x "$filename" ]; then    #  Note the space after the semicolon.
	\#+                   ^^
  		echo "File $filename exists."; cp $filename $filename.bak
	else   #                       ^^
		echo "File $filename not found."; touch $filename
	fi; echo "File test complete."</pre></code>

	Note that the ";" sometimes needs to be escaped.
```	

>`注意『;』符號有時後方需要接上空白。`

;;
Terminator in a case option [double semicolon].
>`雙重『;』也可用做於終止符號。`

```bash
	case "$variable" in
		abc)  echo "\$variable = abc" ;;
		xyz)  echo "\$variable = xyz" ;;
	esac
```

;;&, ;& 
Terminators in a case option (version 4+ of Bash).
>`『;;』與『, ;』在某些版本中也可用做終止符號（4+ Bash版本）。`

"dot" command [period]. Equivalent to source (see Example 15-22). This is a bash builtin.
>`『.』逗點指令，相當於源（見範例15-22），是一個bash的內建命令。`

."dot", as a component of a filename. When working with filenames, a leading dot is the prefix of a "hidden" file, a file that an ls will not normally show.
>`『.』，當逗點作為檔案名稱中的一個元件時，在檔案名稱前的逗點是作為一個『隱藏』檔案的綴飾詞，一個平常使用指令『ls』不會直接顯示的。`

```bash
	bash$ touch .hidden-file
	bash$ ls -l	      
	total 10
 		-rw-r--r--    1 bozo      4034 Jul 18 22:04 data1.addressbook
 		-rw-r--r--    1 bozo      4602 May 25 13:58 data1.addressbook.bak
 		-rw-r--r--    1 bozo       877 Dec 17  2000 employment.addressbook

	bash$ ls -al	      
	total 14
 		drwxrwxr-x    2 bozo  bozo      1024 Aug 29 20:54 ./
 		drwx------   52 bozo  bozo      3072 Aug 29 20:51 ../
 		-rw-r--r--    1 bozo  bozo      4034 Jul 18 22:04 data1.addressbook
 		-rw-r--r--    1 bozo  bozo      4602 May 25 13:58 data1.addressbook.bak
 		-rw-r--r--    1 bozo  bozo       877 Dec 17  2000 employment.addressbook
 		-rw-rw-r--    1 bozo  bozo         0 Aug 29 20:54 .hidden-file
```        

When considering directory names, a single dot represents the current working directory, and two dots denote the parent directory.

>`當確認資料夾名稱時，單獨的一個點『.』代表當前使用者所在的位置，兩個點『..』但表上一層的資料夾位置。`

```bash
	bash$ pwd
	/home/bozo/projects

	bash$ cd .
	bash$ pwd
	/home/bozo/projects

	bash$ cd ..
	bash$ pwd
	/home/bozo/
```

The dot often appears as the destination (directory) of a file movement command, in this context meaning current directory.

>`『.』經常代表著檔案移動的目的地（資料夾），但在這段文字中代表當前的資料夾。`

```bash
	bash$ cp /home/bozo/current_work/junk/* .
```

Copy all the "junk" files to $PWD.

>`複製所有的『垃圾』檔案到$PWD位置。`

.
"dot" character match. When matching characters, as part of a regular expression, a "dot" matches a single character.

>`『.』點，字符配對。當字符配對符合時，點作為一般表達式的一部分，一個『.』代表一個單一字元`

"
partial quoting [double quote]. "STRING" preserves (from interpretation) most of the special characters within STRING. See Chapter 5.

>`「"」雙引號。"STRING"從字元或是文句之中找到大部分特殊字元符合 STRING 的字元。請見單元5。`

'
full quoting [single quote]. 'STRING' preserves all special characters within STRING. This is a stronger form of quoting than "STRING". See Chapter 5.

>`「'」單引號，全匹配。'STRING'從字元或是文句之中找到所有與STRING全匹配的特殊字元。單引號的匹對效果強過雙引號。請見單元5。`

,
comma operator. The comma operator [1] links together a series of arithmetic operations. All are evaluated, but only the last one is returned.
>`「,」逗點，逗點是用作將一連串的算數運算等等所千連在一起的符號。如下方範例所示，只將最後的算式予以回傳。`

>`「逗號」，逗號[1]可用作將一連串的算數運算等等所牽連在一起的符號。如下方範例所示，只將最後的算式予以回傳。`

```bash
	let "t2 = ((a = 9, 15 / 3))"
	# Set "a = 9" and "t2 = 15 / 3"
```

The comma operator can also concatenate strings.

>`逗號也可用作連接字串。`

```bash
	for file in /{,usr/}bin/*calc
	#             ^    Find all executable files ending in "calc"
	#+                 in /bin and /usr/bin directories.
	do
        	if [ -x "$file" ]
        	then
        		echo $file
        	fi
	done

 	# /bin/ipcalc
 	# /usr/bin/kcalc
 	# /usr/bin/oidcalc
 	# /usr/bin/oocalc


	# Thank you, Rory Winston, for pointing this out.
```
,, ,
Lowercase conversion in parameter substitution (added in version 4 of Bash).
>`「,,」以及「,」在參數替換中用作小寫轉換代表（於版本四中的Bash新增）`

\
escape [backslash]. A quoting mechanism for single characters.
>`「\」跳脫字元［反斜線］，一個具有引用機制的單個字元`

\x escapes the character X. This has the effect of "quoting" X, equivalent to 'X'. The \ may be used to quote " and ', so they are expressed literally.
>`「\x」代表X從單純的字元「X」中跳脫出，而具有不同的意思，相當於「'X'」。「\」可以用於代表引用符號「"」與「'」，從而可使兩者符號被更仔細的區分。`

See Chapter 5 for an in-depth explanation of escaped characters.
>`可查閱第五章，獲得更詳細關於跳脫字元的解釋。`

/
Filename path separator [forward slash]. Separates the components of a filename (as in /home/bozo/projects/Makefile).
>`「/」文件路徑分隔符號［斜線］，用作分隔文件路徑的元件（例如：/home/bozo/projects/Makefile）。`

This is also the division arithmetic operator.
>`這也同樣是算數中相除的符號。`

`
command substitution. The `command` construct makes available the output of command for assignment to a variable. This is also known as backquotes or backticks.
>`「`」命令替換。「`command`」建構使得一般命令可作為變數的輸出。符號同時也被稱為反引號或是反勾。`

:
null command [colon]. This is the shell equivalent of a "NOP" (no op, a do-nothing operation). It may be considered a synonym for the shell builtin true. The ":" command is itself a Bash builtin, and its exit status is true (0).
>`「:」空白命令［冒號］，在shell之中是作為一個不進行任何事物的操作指令英文簡寫為"NOP"（no op，無操作）。冒號同時也被認定在shell的內置外殼，冒號是Bash中一個內置的命令，相當於true。`

```bash
	:
	echo $?   # 0
```

Endless loop:
>`無限迴圈：`

```
while :
do
   operation-1
   operation-2
   ...
   operation-n
done

# Same as:
#    while true
#    do
#      ...
#    done
```

Placeholder in if/then test:
>`於判斷循環中的暫駐測試：`

```
if condition
then :   # Do nothing and branch ahead
else     # Or else ...
   take-some-action
fi
```

Provide a placeholder where a binary operation is expected, see Example 8-2 and default parameters.
>`於二進位運算發生時提供暫駐行為。可在範例8-2與一般變數中看到參考。`

```
: ${username=`whoami`}
# ${username=`whoami`}   Gives an error without the leading :
#                        unless "username" is a command or builtin...

: ${1?"Usage: $0 ARGUMENT"}     # From "usage-message.sh example script.
```

Provide a placeholder where a command is expected in a [here document](http://tldp.org/LDP/abs/html/here-docs.html#HEREDOCREF). See Example 19-10.
>`在 here document 命令之中提供一個暫駐，見範例19-10。`

Evaluate string of variables using parameter substitution (as in Example 10-7).
>`使用參數替換評估字符串變量（如範例10-7）。`

```
: ${HOSTNAME?} ${USER?} ${MAIL?}
#  Prints error message
#+ if one or more of essential environmental variables not set.
```
Variable expansion / substring replacement.
>`變數延伸 / 字串替換`

In combination with the > redirection operator, truncates a file to zero length, without changing its permissions. If the file did not previously exist, creates it.
>`在與重新定向操作符「>」的結合，將文件截為零資料長度，同時不改變檔案的權限。假若檔案之前並不存在，則將其創建。`

```
: > data.xxx   # File "data.xxx" now empty.	      

# Same effect as   cat /dev/null >data.xxx
# However, this does not fork a new process, since ":" is a builtin.
```
See also Example 16-15.
>`請見範例 16-15。`

In combination with the >> redirection operator, has no effect on a pre-existing target file (: >> target_file). If the file did not previously exist, creates it.
>`與重新指向符號「>>」合併使用，對先前存在的指向位置檔案(: >> 目標檔案)無效。假若檔案不存在，則創建它。`

Note	
This applies to regular files, not pipes, symlinks, and certain special files.

May be used to begin a comment line, although this is not recommended. Using # for a comment turns off error checking for the remainder of that line, so almost anything may appear in a comment. However, this is not the case with :.
```
: This is a comment that generates an error, ( if [ $x -eq 3] ).
```
The ":" serves as a field separator, in /etc/passwd, and in the $PATH variable.
```
bash$ echo $PATH
/usr/local/bin:/bin:/usr/bin:/usr/X11R6/bin:/sbin:/usr/sbin:/usr/games
```
A colon is acceptable as a function name.
```
:()
{
  echo "The name of this function is "$FUNCNAME" "
  # Why use a colon as a function name?
  # It's a way of obfuscating your code.
}

:

# The name of this function is :
```
This is not portable behavior, and therefore not a recommended practice. In fact, more recent releases of Bash do not permit this usage. An underscore _ works, though.


A colon can serve as a placeholder in an otherwise empty function.
```
not_empty ()
{
  :
} # Contains a : (null command), and so is not empty.
```
!
reverse (or negate) the sense of a test or exit status [bang]. The ! operator inverts the exit status of the command to which it is applied (see Example 6-2). It also inverts the meaning of a test operator. This can, for example, change the sense of equal ( = ) to not-equal ( != ). The ! operator is a Bash keyword.

In a different context, the ! also appears in indirect variable references.

In yet another context, from the command line, the ! invokes the Bash history mechanism (see Appendix L). Note that within a script, the history mechanism is disabled.

*
wild card [asterisk]. The * character serves as a "wild card" for filename expansion in globbing. By itself, it matches every filename in a given directory.
```
bash$ echo *
abs-book.sgml add-drive.sh agram.sh alias.sh
```	      

The * also represents any number (or zero) characters in a regular expression.

*
arithmetic operator. In the context of arithmetic operations, the * denotes multiplication.

** A double asterisk can represent the exponentiation operator or extended file-match globbing.

?
test operator. Within certain expressions, the ? indicates a test for a condition.


In a double-parentheses construct, the ? can serve as an element of a C-style trinary operator. [2]

condition?result-if-true:result-if-false
```
(( var0 = var1<98?9:21 ))
#                ^ ^

# if [ "$var1" -lt 98 ]
# then
#   var0=9
# else
#   var0=21
# fi
```
In a parameter substitution expression, the ? tests whether a variable has been set.

?
wild card. The ? character serves as a single-character "wild card" for filename expansion in globbing, as well as representing one character in an extended regular expression.
