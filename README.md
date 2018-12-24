# One-liners

Useful bash one-liners.

[TOC levels=1-3]: # " "

- [One-liners](#one-liners)
- [References:](#references)
- [Basic bash tools](#basic-bash-tools)
    - [`cat`, `sort`, `uniq`, `cut`, etc.](#cat-sort-uniq-cut-etc)
- [Terminal appearances](#terminal-appearances)
    - [使用 Xterm 控制序列改变终端大小](#使用-xterm-控制序列改变终端大小)


# References:

* http://www.commandlinefu.com/
* https://github.com/stephenturner/oneliners/
* http://genomespot.blogspot.com/2013/08/a-selection-of-useful-bash-one-liners.html

# Basic bash tools

##  `cat`, `sort`, `uniq`, `cut`, etc.

[[back to top](#one-liners)]

Number each line in file.txt:

```bash
cat -n file.txt
```

Count the number of unique lines in file.txt

```bash
cat file.txt | sort -u | wc -l
```

# Terminal appearances


## 使用 Xterm 控制序列改变终端大小

https://apple.stackexchange.com/a/47841

Set the window to 100x30 characters:

```bash
printf '\e[8;30;100t'
```

Move the window to the top/left corner

```bash
printf '\e[3;0;0t'
```

