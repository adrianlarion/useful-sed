# Useful sed scripts



###### print one line
`sed -n '10p' myfile.txt` 

###### do replacement on all lines except line 5
`sed '5!/s/foo/bar/' file.txt`


###### Print lines between two regexes
`sed -nr '/^foo/,/^bar/p' file.txt`

###### Use custom delimiters to make it easy for some strings that contain slashes
`sed 's_/bin/bash_/bin/sh' file.txt ` 

###### Insert a space between lowercase/Uppercase characters using & (which represents the regex match)
`sed 's/[a-zA-Z]/& /g' file.txt `

###### keep the first word of every line
`sed -r s_[a-z]+.*_\1_' file.txt `


###### switch the first two words 
`sed -r 's_([a-zA-Z]*) ([a-zA-Z]*)_\2 \1_' f1`

