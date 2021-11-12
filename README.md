# Useful sed scripts



#### print one line
`sed -n '10p' myfile.txt` 

#### do replacement on all lines except line 5
`sed '5!/s/foo/bar/' file.txt`

#### do replacement on lines matching regex (eg: lines starting with 'hello')
`sed '/^hello/ s/h/H/' file.txt ` 



#### do replacement from line 5 to end of file
`s '1,$ s/foo/bar/' file.txt `

#### Print lines between two regexes
`sed -nr '/^foo/,/^bar/p' file.txt`

#### Use custom delimiters to make it easy for some strings that contain slashes
`sed 's_/bin/bash_/bin/sh_' file.txt ` 

#### Insert a space between lowercase/Uppercase characters using & (which represents the regex match)
`sed 's/[a-zA-Z]/& /g' file.txt `

#### keep the first word of every line
`sed -r s_[a-z]+.*_\1_' file.txt `


#### switch the first two words 
`sed -r 's_([a-zA-Z]*) ([a-zA-Z]*)_\2 \1_' f1`


#### remove duplicate words (but not triplicate)
`sed -r 's_([a-z]+) \1_\1_ig' f1`

#### search and replace for pattern, write just the lines with the replacements in a new file
`sed -r 's_foo_bar_w replaced.txt' file.txt  `

#### multiple replacements
`sed -e 's_foo_bar_' -e 's_hello_HELLO_' file.txt `

#### multiple replacements by using a bash script
```
#!/bin/bash
sed '
s/a/A/
s/foo/BAR/
s/hello/HELLO/
' <$1
```
* call with  `./myscript.sh myfile.txt`


#### remove comments between lines starting with these two keywords
`sed -r '/start/,/end/ s/#.*//' file.txt `

#### view lines minus lines between line starting with pattern and end of file 
`sed -r '/start/,$ d' file.txt `

#### view lines except lines between line starting with pattern and line ending with pattern
`sed -rn '/start/,/end/ !p' file.txt `

#### print until you encounter pattern then quit
`sed -r '/start/q' file.txt `

#### insert contents of file after a certain line
`sed -r '5 r newfile.txt' file.txt `

#### Append text after lines containing regex (AFTER FOO)
`sed '/foo/ a AFTER FOO' file.txt `

#### Insert text after lines containing regex (BEFORE FOO)
`sed '/foo/ i BEFORE FOO' file.txt `

#### change line containing regex match
`sed '/foo/c FOO IS CHANGED' file.txt `

#### Nested sed ranges with inversion. Between lines 1,100 apply actions where the pattern DOESN'T match.
```
#!/bin/bash
sed  '
1,100 {
	/foo/ !{
		s_hello_HELLO_
		s_yes_YES
	}
}'
```
* call with `./script.sh <file.txt `


#### Use nested addresses with change, insert and append to modify: the line before match, the line with match, the line after match.
```
#!/bin/bash
sed '
/^#/ {
i\
#BEFFORE ORIGINAL COMMENt
a\
#AFTER ORIGINAL COMMENT
c\
# ORIGINAL COMMENT IS NOW THIS LINE
}'

```

#### Insert new line before the first comment, after the first comment put in the contents of file and quit immediately afterwards
```

#!/bin/bash
sed '
/^#/ {
i #BEFORE COMMENT
r myotherfile.txt
q
}'
```

#### Transform text 
`sed 'y/abc/ABC/' file.txt `


#### Copy all the comments (starting with #) to a new file
`sed -r '/^#/w comments.txt' file.txt `

#### Print every second line (substitute ~3 for third line, etc)
`sed '1~2p' file.txt `

#### Edit file in place but also create a backup
`sed -i.bak 's/hello/HELLO/' file.txt `

