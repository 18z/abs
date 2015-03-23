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

\
escape [backslash]. A quoting mechanism for single characters.

\x escapes the character X. This has the effect of "quoting" X, equivalent to 'X'. The \ may be used to quote " and ', so they are expressed literally.

See Chapter 5 for an in-depth explanation of escaped characters.

/
Filename path separator [forward slash]. Separates the components of a filename (as in /home/bozo/projects/Makefile).

This is also the division arithmetic operator.

`
command substitution. The `command` construct makes available the output of command for assignment to a variable. This is also known as backquotes or backticks.

:
null command [colon]. This is the shell equivalent of a "NOP" (no op, a do-nothing operation). It may be considered a synonym for the shell builtin true. The ":" command is itself a Bash builtin, and its exit status is true (0).
```bash
	:
	echo $?   # 0
```
