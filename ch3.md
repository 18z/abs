第三章 特殊字元
---
What makes a character special? If it has a meaning beyond its literal meaning, a meta-meaning, then we refer to it as a special character. Along with commands and keywords, special characters are building blocks of Bash scripts.

>`是什麼讓字元特殊呢？假設他擁有超出其字面意義的意思，一個精粹的意思，那麼我們將它作為一個特殊字元。與其他命令與關鍵字詞被建築在Bash腳本之中。`

Special Characters Found In Scripts and Elsewhere

>`特殊字元可以在腳本或是其它地方中被發現`

Comments. Lines beginning with a (with the exception of ) are comments and will not be executed.

<pre><code># This line is a comment.</pre></code>

Comments may also occur following the end of a command.

<pre><code> echo "A comment will follow." # Comment here.
 #                            ^ Note whitespace before #</pre></code>

Comments may also follow whitespace at the beginning of a line.

 <pre><code>    # A tab precedes this comment.</pre></code>
Comments may even be embedded within a pipe.

<pre><code> initial=( `cat "$startfile" | sed -e '/#/d' | tr -d '\n' |\
 # Delete lines containing '#' comment character.
           sed -e 's/\./\. /g' -e 's/_/_ /g'` )
 # Excerpted from life.sh script</pre></code>
