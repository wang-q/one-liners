# One-liners

Useful bash one-liners.

[TOC levels=1-3]: # " "

- [One-liners](#one-liners)
- [References:](#references)
- [Basic bash tools: `cat`, `sort`, `uniq`, `cut`, etc.](#basic-bash-tools-cat-sort-uniq-cut-etc)


# References:

* http://www.commandlinefu.com/
* https://github.com/stephenturner/oneliners/
* http://genomespot.blogspot.com/2013/08/a-selection-of-useful-bash-one-liners.html

# Basic bash tools: `cat`, `sort`, `uniq`, `cut`, etc.

[[back to top](#one-liners)]

Number each line in file.txt:

    cat -n file.txt

Count the number of unique lines in file.txt

    cat file.txt | sort -u | wc -l

