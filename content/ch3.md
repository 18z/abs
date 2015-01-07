第三章 特殊字元
---
What makes a character special? If it has a meaning beyond its literal meaning, a meta-meaning, then we refer to it as a special character. Along with commands and keywords, special characters are building blocks of Bash scripts.

>`是什麼讓字元特殊呢？假設他擁有超出其字面意義的意思，一個精粹的意思，那麼我們將它作為一個特殊字元。與其他命令與關鍵字詞被建築在Bash腳本之中。`

Special Characters Found In Scripts and Elsewhere

>`特殊字元可以在腳本或是其它地方中被發現`

Comments. Lines beginning with a (with the exception of ) are comments and will not be executed.

>`註解。句子開頭加上符號（如例子所示的『#』），代表這句子是註解並不會被執行。`

<pre><code># This line is a comment.</pre></code>

Comments may also occur following the end of a command.

>`註解也會出現在命令句的後方。`

<pre><code> echo "A comment will follow." # Comment here.
 #                            ^ Note whitespace before #</pre></code>

Comments may also follow whitespace at the beginning of a line.

>`註解的符號後方也可以先接上空白再開始整個句子。`

 <pre><code>    # A tab precedes this comment.</pre></code>

Comments may even be embedded within a pipe.

>`註解甚至也可以在斜線中插入。`

<pre><code> initial=( `cat "$startfile" | sed -e '/#/d' | tr -d '\n' |\
 # Delete lines containing '#' comment character.
           sed -e 's/\./\. /g' -e 's/_/_ /g'` )
 # Excerpted from life.sh script</pre></code>

A command may not follow a comment on the same line. There is no method of terminating the comment, in order for "live code" to begin on the same line. Use a new line for the next command.
	
Of course, a quoted or an escaped # in an echo statement does not begin a comment. Likewise, a # appears in certain parameter-substitution constructs and in numerical constant expressions.
<pre><dode>echo "The # here does not begin a comment."
echo 'The # here does not begin a comment.'
echo The \# here does not begin a comment.
echo The # here begins a comment.</pre></code>

echo ${PATH#*:}       # Parameter substitution, not a comment.
echo $(( 2#101011 ))  # Base conversion, not a comment.

# Thanks, S.C.
The standard quoting and escape characters (" ' \) escape the #.

Certain pattern matching operations also use the #.

;
Command separator [semicolon]. Permits putting two or more commands on the same line.

echo hello; echo there


if [ -x "$filename" ]; then    #  Note the space after the semicolon.
#+                   ^^
  echo "File $filename exists."; cp $filename $filename.bak
else   #                       ^^
  echo "File $filename not found."; touch $filename
fi; echo "File test complete."

Note that the ";" sometimes needs to be escaped.

;;
Terminator in a case option [double semicolon].

case "$variable" in
  abc)  echo "\$variable = abc" ;;
  xyz)  echo "\$variable = xyz" ;;
esac

;;&, ;&
Terminators in a case option (version 4+ of Bash).

.

"dot" command [period]. Equivalent to source (see Example 15-22). This is a bash builtin.

.
"dot", as a component of a filename. When working with filenames, a leading dot is the prefix of a "hidden" file, a file that an ls will not normally show.
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
	        

When considering directory names, a single dot represents the current working directory, and two dots denote the parent directory.

bash$ pwd
/home/bozo/projects

bash$ cd .
bash$ pwd
/home/bozo/projects

bash$ cd ..
bash$ pwd
/home/bozo/
	        
The dot often appears as the destination (directory) of a file movement command, in this context meaning current directory.
