---
layout:     post
title:      "Command line text processing"
subtitle:   "命令行文本处理"
date:       2020-04-01 11:42:00
author:     "aguozhang"
header-img: "img/post-bg-2015.jpg"
tags:
    - Command line
    - text
    - sed 
    - awk

    - 
---


## 前言
作为一个程序开发人员，熟悉使用命令行，尤其中文本处理方面的，是一个基本的要求, 它可以帮助你大大提高效率。

就像你有一个工具箱，里面有各种各样的工具了，遇到问题使用合适的工具。

没有这个工具箱，就会出现，你只有一把锤子, 就不可避免的出现把所有问题都看成钉子。

github有一个库，把文本命令行的方面讲得很详细，[链接](https://github.com/learnbyexample/Command-line-text-processing)


## 摘录

### cat
* cat marks_201*
* cat - marks_2015.txt
* printf 'hello\n\nworld\n\nhave a nice day\n'
* cat -n marks_201* 
* cat -sb mark_201*
* nl
* cat -E marks_2015.txt
* cat -T marks_2015.txt
* printf 'foo\0bar\0baz\n' | cat -v
* -A is equivalent to -vET
* -e is equivalent to -vE
* cat > abc.txt

### tac
* tac report.log | sed -n '/Error:/,/Warning:/p' | tac
* line reverse use rev
* grep -E 'Warning|Error' report.log
* tr 'A-Z' 'a-z' < marks_2015.txt
* grep -c 'foo' marks_201*
* cat marks_201* | grep -c 'foo'
* Use input redirection if a command doesn't accept file input

### less
* g go to start of file
* G go to end of file
* q quit
* /pattern search for the given pattern in forward direction
* ?pattern search for the given pattern in backword direction
* n go to next pattern
* N go to previous pattern

### tail
* Use -n option to control number of lines to filter
* when number is prefixed with + sign, all lines are fetched from that particular line number to end of file
* tail -c3
* tail -c +2
* tail -n2 report.log sample.txt
* tail -q -n2 report.log sample.txt
* tail -f

### head
* head sample.txt
* head -n3 sample.txt
* when number is prefixed with - sign, all lines are fetched except those many lines to end of file
* head -c2
* head -c -4

### grep
* echo 'int a[5]' | grep 'a[5]' 
* echo 'int a[5]' | grep -F 'a[5]'
* or fgrep
* grep -i
* grep -v
* grep -n
* grep -c  // count number of matching lines
* grep -m2 // Limit number of matching lines
* grep -e 'blue' -e 'you' poem.txt  // search blue or you
* grep -if search_strings.txt poem.txt  // -f option accept file input with search terms in separat lines
* grep 'are' poem.txt | grep 'And'  // match line containing both are & And
* grep -l // -l to get files matching the search
* grep -L // -L to get files not matching the search
* grep -h // -h is default for single file input, no file name prefix in output
* grep -H // -H is default for multiple file input, file name prefix in output
* grep -w 'par' // match whole word
* grep -x // -x to match only complete line, not anywhere in the line
* grep --color=  // auto  always never
* grep -o  // Get only matching portion
* grep -A -B -C 
* grep -A 1  // By default adds a line -- to separate them
* Note: exclusion/inclusion applies only to basename of file/directory, not the entire path
* Follow all symbolic links use -R
* bash globstar
* grep -d skio -il 'yellow' **/*
* grep rlZ 'you' | xargs -0 awk '{print $1}'
* grep -rlZ 'you' | xargs -0 grep -L 'are'
* -F option will force matching strings literally(no regular expressions)
* grep -Fxvf test_files/colors.txt test_files/vibgyor.txt
* -q for exit status, 0 if matched else non0
* The -E option allows to use ERE(Extended Regular Expression) which in GNU grep's case only differs in how meta characters are used, no difference in regular expression functionalities
* -P which indicates PCRE
* The matched string within () can also be used to be matched again by backer referencing the captured groups
* \1 denotes the first matched group, \2 the second one and so on
* grep -xE '([a-d]..)\1' /usr/share/dict/words
* printf 'red\nblue\n\0green\n' | grep -z 'red'

### sed
* sed -i.bkp 's/Hi/Hello/' greeting.txt
* * also allows to specify an existing directory to place the backups instead of current working directory
* sed -i 'bkp_dir/*' 's/bar/hi/' var.txt
* By default, sed prints ever4y input line, including any changes made by commands like substitution
* Using -n option and p command together, only specific lines needed can be filtered
* sed -n 's/are/ARE/p' poem.txt
* sed -n '/are/ s/so/SO/p' poem.txt
* sed '/are/d' poem.txt
* sed '/rose/Id' poem.txt
* remember that printing is default action if -n is not used
* Use ! to invert the specified address
* sed '/so are/!d' poem.txt
* sed -n '2p' poem.txt
* sed -n '2p; 4p' poem.txt
* sed -n '/just/I,/believe/Ip' addr_range.txt
* sed -n '3,7p' addr_range.txt
* 1~2 means 1st, 3rd, 5th, 7th, etc(i.e odd numbered lines)
* By default, sed treats REGEX as BRE(Basic Regular Expression)
* The -E option enables ERE
* Substitute command modifiers
* g p I
* w modifier Allow to write only the changes to specified file name instead of default stdout
* seq 20 | sed -n 's/3/three/w 3.txt' 
* e modifier Allow to use shell command output in REPLACEMENT section
* printf 'Date:\nreplace this line\n' | sed 's/^replace.*/date/e'
* word='are' 
* sed -n "/$word/p" poem.txt

### awk
* gawk - pattern scanning and processing language
* $0 contains the entire input record
* $1 contains the first field text
* default input field separator is one or more of continuous space, tab or newline characters
* $(2+3)
* NF
* awk '{print $1}' fruits.txt
* Input field separator -F or FS variable
* echo 'foo:123:bar:789' | awk -F: '{$2}'
* echo 'Sample243qwew3ls4564323klise' | awk -F'[0-9]+' '{print $2}'
* assigning empty string to FS will split the input record character wise
* note the use of command line option -v to set FS
* echo 'apple' | awk -v FS= '{print $1}'
* by setting OFS variable
* echo 'foo:123:bar:789' | awk 'BEGIN{FS=OFS=":"} {print $1, $NF}'
* print statement with no arguments will print contents of $0
* if condition is specified without corresponding statements, contents of $0 is printed if condition evaluates to true
* 1 is typically used to represents always true condition and thus print contents of $0
* awk '$1=="apple"{print $2}' fruits.txt
* The REGEXP is specified with // and by default acts upon $0
* awk '/are/' poem.txt
* awk '/are/{print $NF}' poem.txt
* awk '$1 ~ /a/' fruits.txt
* awk '$1 !~ /a/' fruits.txt
* to search a string literally, index function can be used instead of REGEXP
* awk 'index($0, "a+b")==1' eqns.txt
* awk 'NR==2 || NR==4' poem.txt
* awk -v RS=' ' '{print NR, $0}'
* ORS to change output record separator
* seq 3 | awk -v ORS='\n\n' '{print $0}'
* sub replacing first occurence, gsub for replacing all occurences
* echo '1-2-3-4-5' | awk '{sub("-", ":")} 1'
* awk 'BEGIN{print ENVIRON["PWD"]}'
* r='[^-]'
* echo '1-2-3-4-5' | awk -v r="$r" '{gsub(r, "abc")} 1'

### sort
* sort lines of text files
* grep -oi '[a-z]*' poem.txt | LC_ALL=C sort
* sort -r poem.txt
* sort -n numbers.txt
* The <() syntax is Process Substitution
* sort -n numbers.txt <(echo '-4')
* Use -g if input contains numbers prefixed by + or E scientific notation
* du sort -h
* du -sh * | sort -h
* If this sorting is needed simply while displaying directory contents, use ls -v instead of piping to sort -V
* sort -V versions.txt
* sort -R  === shuf
* sort -R nums.txt -o rand_nums.txt
* for f in *.txt; do echo sort -V "$f"c -o "$f"; done
* sort -u
* -f option to ignore case of alphabets while determining duplicates
* Column based sorting -k pos1[, pos2]
* sort -t: -k2,2 pets.txt
* sort -t, -k2.4,2n marks.txt

### uniq
* report or omit repeated lines
* uniq -d word_list.txt # duplicates adjacent to each other
* uniq -D word_list.txt  # To get only duplicates as well as show all duplicates
* sort word_list.txt | uniq --all-repeated=separate  # To distinguish the different groups
* uniq -u wordlist.txt # lines with no adjacent duplicates
* sort word_list.txt | uniq -u
* uniq -c word_list.txt # prefix count, adjacent lines
* sort word_list.txt | uniq -c | sort -n
* sort colors.txt | uniq -c | sort -nr | awk 'NR==1{c=$1} $1==c'  ## to get all max count, save 1st line 1st column value to c and then print if 1st column equals c
* sort colors.txt | uniq -c | sort -n | awk 'NR==1{c=$1} $1==c'
* awk '{primt $1}' "$HISFILE" | sort | uniq -c | sort -nr | head
* grep -oP '(^; +\| +)\K[^ ]+' "$HISTFILE" | sort | uniq -c | sort -nr | head
* uniq -i # ignore case


### comm
* compare two sorted files line by line
* paste colors_1.txt colors_2.txt


### shuf
* generate random permutations
* Write a random permutation of the input lines to standard output
* shuf nums.txt
* shuf -n2 nums.txt
* shuf nums.txt -o nums.txt

### paste
* merge lines of files
* paste colors_1.txt colors_2.txt  # By default, paste adds a TAB between corresponding lines of input files
* Specifying a diffenent delimiter using -d
* <() Process Substitution
* Input lines can be passed only as stdin

### column
* columnate lists
* The column utility formats its input into multiple columns. Row are filled before columns. Input is take from file operands, or , by default, from the standard input. Rmpty limes are ignored unless the -e option is used. 
* column -t dishes.txt

### pr
* convert text files for printing

### fold
* wrap each input line to fit in specified width

### cmp
* compare two files byte by byte

### diff 
* compare files line by line

### wc 
* print newline, word, and byte counts for each file
* use -L to get length of longest line
* wc -L < sample.txt
* wc -c byte count
* wc -m character count

### du
* estimate file space usage
* du
* -a recursively show both files and directories
* -s to show total directory size without descending into its sub-directories
* du -a
* du -s
* use -S to show directory size without taking into account size of its sub-directories
* stat -c %s words.txt
* du -b words.txt
* du -sk projs
* du -sm projs
* human readable and si units
* du -sh projs/* words.txt
* du -s --si projs/* words.txt
* du -sh projs/* words.txt | sort -h
* -d to specify maximum depth
* -c to also show total size at end
* -t to provide a threshold comparison

### df
* report file system disk space usage
* df .
* df -h .

### touch 
* change file timestamps
* use -c if new file shouldn't be created
* touch -c foo.txt

### file
* determine file type
* file sample.txt
* file -b sample.txt  ## without file name in output

### cut
* remove sections from each line of files
* Default delimiter is tab character
* -f option allows to print specific fields from each input line
* cut -f2
* cut -f2,4
* cut -f3-
* use -d option to specify input delimiter other than dfault tab character
* only single character can be used, for multi-character/regex based delimiter use awk or perl
* cut -d: -f3
* use --output-delimiter option to specify differnet output delimiter

### tr
* translate or delete character
* tr 'abc' '123'
* tr ';' ':'
* tr 'a-z' 'n-za-m'
* use shell input direction for file input
* tr 'a-z' 'A-Z' < marks.txt
* #when second argument is longer, the extra characters are ignored
* tr 'abc' '1-9' 
* when first argument is longer the last character of second argument get re-used
* tr 'a-z' '123'
* ust -t option to truncate first argument to same length as second
* tr -t 'a-z' '123'
* use -- to indicate end of option processing
* similarly, to represent \ literally, use \\
* use -d option to specify characters to be deleted
* add complement option -c if it is easier to define which characters are to be retained
* echo '2017-03-21' | tr -d '-'
* # retain only alphabets, comma and newline characters
* echo '"Foo1!", "Bar.", ":Baz:"' | tr -cd '[:alpha:],\n'

### basename
* strip directory and suffix from filenames
* use -a option if there are multiple arguments
* basename -a fool/a/report.log bar/y/power.log
* use suffix option -s to strip file extension from filename
* basename -s '.log' '/home/learnbyexample/proj adder/power.log'   
* power


### dirname
* strip last component fro file name
* dirname foo/a/report.log bar/y/power.log
* Use $() command substitution to further process output as needed
* basename "$(dirname '/home/learnbyexample/proj adder/power.log')"

### xargs
* build and execute command lines from standard input
* While xargs is primarily used for passing output of command or file contents to another command as input arguments and/or parallel processing, it can be quite handy for certain text processing stuff with default echo command
* -n option limits number of arguments per line
* use -a option to specify file input instead of stdin
* use -L option to limit max number of lines per command line
* since echo is the command being executed, it will cause issue with option interpretation
* use -t option to se what is happening, verbose output


### seq
* print a sequence of numbers
* seq 3

### find  
* search for files in a directory hierachy
* find -not -name '*log'   print path of 
* find -regextype -egrep -regex '.*/\w+'  # use extended regular expression to matcvh filename containing only [a-zA-Z_] character, .*/ is needed to match initial part of file path
* The relative path . is considered as depth 0 directory, files and folders immediately contained in a directory are at depth 1 and so on
* find -maxdepth 1 -type f
* find -maxdepth 1 -type f -name '[!.]*'
* find report -name '*log*' -exec rm {} \; delete all filenames containing log in report folder and its sub-folders; here rm command is called for every file matching the search conditions; since ; is a special character for shell, it needs to be escaped using \
* find -name '*.txt' -exec wc {} + list of files ending with txt are all passed together as argument to wc command instead of executing wc command for every file; no need to use escape the + character in this case; also note that number of invocations of command specified is not necessarily once if number of files found is too large

### locate
* find files by name
* locate 'power'
