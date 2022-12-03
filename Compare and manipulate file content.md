# Compare and manipulate file content

## Regular Expressions

Regular Expressions are text patterns that are used by tools like grep and others.

*Don't confuse regular expressions with globbing!* They may look like expressions with globbing, but are really different.

``grep 'a*' or a*``
a* is globbing, 'a*' is a Regular Expression.  

Regular expressions are used with specific tools only like grep, vim, awk and sed. **Extended** regular expressions enhance basic regex features. See man 7 regex for details.

Regular expressions are built around **atoms**; an atom specifies what text is to be matched. Atoms can be single characters, a range of characters, or a dot. 

Atoms can also be a class, such as \[[:alpha:\]], \[[:digit:\]] or \[[:alnum:\]]. 

Second is the repetition operator, specifying how often a character occurs. The third element is indicating where to find the next character.

This searches the regtext file for anything beginning with b and ends with t. The dot is a wildcard charachter.
``grep 'b.t' regtext``  

If we do grep 'b.\*t' regtext. The * functions as a repitition operator. 

Here are some operators we can use.

-   ^ beginning of the line.  
-   $ end of line. 
-   \< beginning of word. 
-   \> end of word. 
-   * Zero or more times. 
-   + one or more times. 
-   ? zero or one time. 
-   {n} exactly n time. 

## Grep options

|   |   |
|---|---|
|-i   | Not case sensitive. Matches upper- and lowercase letters.  |
|-v   | Shows only lines that do not contain the regular expression.   |
|-r   | Searches files in the current directory and all subdirectories.    |
| -e | Searches for lines matching more than one regular expression. |
| -A \<number> | Shows \<number> of lines after the matching regular expression. |  
| -B \<number> | Shows \<number> of lines before the matching regular expression. |

### Examples

``grep '\<root\>' * 2>/dev/null``

Show us all files in the working directory that have only three characters in their name.  
``grep '^...$' *``   

### Extended Regular Expressions 

If we want to do ``grep 'b.?t'`` regtext we must use an **extended regular expression**.
Those types of expressions start with **egrep**, not grep. 

## CUT and SORT

### Examples

#### CUT

Pipe the output of the third field in "/etc/passwd" to less. The delimeter between fields is ":"".
``cut -f 3 -d : /etc/passwd | less``

Here we use space as the delimiter.

``cut -d ' ' -f 1 userinfo.txt``

This command cuts the first field and changes everything in lowercase to uppercase.
``cut -d : -f 1 /etc/passwd | tr [:lower:] [:upper:]`` 

#### SORT

Cut out the first field in the "passwd" file and sort it alphabetically.
``cut -f 1 -d : /etc/passwd | sort``

How to remove duplicate lines when using sort.

``sort oscarwinners.txt | uniq``


## AWK

``awk -F : '/linda/ { print $4 }' /etc/passwd``

``ps aux | awk '{print $NF }'``

## SED

Switch out four for FOUR globally in the file "sedfile".
``sed -i s/four/FOUR/g sedfile``

``sed -i -e '2d' sedfile``

Shows the fith line in passwd.
``sed -n 5p /etc/passwd/``

Deletes line 2, 20 and 25 from myfile.
``sed -i -e '2d;20,25d' ~/myfile`

## Random commands

### DIFF
To see the differences between two files.

``diff file1 file2``

To see context around lines that differ.

``diff -c file1 file2``

Easiest way is to use a side-by-side comparison of two files. You can use ``diff -y`` or ``sdiff`` both accomplish the same thing.

``diff -y file1 file2``

### GREP

Search a directory for "centos". -i stands for case insensitive. -r is recursive.

``grep -ir "centos" /etc/``

To match only whole words not parts of words use the -w option.

``grep -iw "red" /etc/`` This would not output anything that says "redhat". Only "red" and it also ignores the case because of the -i option.