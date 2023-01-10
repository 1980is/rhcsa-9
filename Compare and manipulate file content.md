# Compare and manipulate file content

## Extended Regular Expressions 

Checkout out [regexr.com](https://regexr.com/) for more information.

If we want to do e.g., ``grep 'b.?t'`` we should use an **extended regular expression**.
Those types of expressions start with **egrep**, not grep.

In basic regular expressions the meta-characters ?, +, {, |, (, and ) lose their special meaning; instead use the backslashed (escaped) versions \\?, \\+, \\{, \\|, \\(, and \\). **It's easier to always use egrep and not grep**, then you don't have to escape the meta-characters.

``egrep -r "0{3,}" /etc/``

This gives us anything matching at least three zeros in "/etc/".
If we wanted to use a regular expression we would have to escape the {} characters.

``grep -r "0\{3,\}" /etc/``

To search files in "/etc/" for the word "disabled". The ? character means that the "d" in disabled can exist once or zero times. So it would return words like, "disabled" or "disable".

``egrep -r "disabled?" /etc/

This searches "/etc/" for either disabled or enabled.

``egrep -r "enabled|disabled" /etc/``

Search in the "/dev/" directory for any file that begins with a-z, and has another character zero or more times, has a number from 0-9, and ends with any character

``egrep -r "/dev/[a-z]\*[0-9]?" /etc/``

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

If we do ``grep 'b.\*t' sometextfile``. The * functions as a repitition operator.

We use \\ to escape special characters so that Bash doesn't interpret them.
Let's say we want to find all periods in "/etc/login.defs". If we did ``grep "." /etc/login.defs`` grep would return the whole document since the period operator functions as "match any one character" as we can see below. We would fix this by escaping the period.

If we do this, only the periods in the document are highlighted red. ``grep "\." /etc/login.defs`` 

**Repetition**

Here are some operators we can use for repition.

A regular expression may be followed by one of several repetition operators:

- ? The preceding item is optional and matched at most once.
- \* The preceding item will be matched zero or more times.
- \+ The preceding item will be matched one or more times.
- {n} The preceding item is matched exactly n times.
- {n,} The preceding item is matched n or more times.
- {,m} The preceding item is matched at most m times. This is a GNU extension.
- {n,m} The preceding item is matched at least n times, but not more than m times.

**Other operators**

-   ^ beginning of the line.  
-   $ end of line. 
-   \< beginning of word. 
-   \> end of word.  
-   .  match any ONE character.
-   | is an or operator.

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

Count how many numbers begin with 2 in "textfile".

``grep -c '^2' textfile``


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
This searches for lines with /linda/ and prints out field number 4.

``ps aux | awk '{print $NF }'``

## SED

Switch out four for FOUR globally in the file "sedfile".

``sed -i s/four/FOUR/g sedfile``

Shows the fith line in passwd.

``sed -n 5p /etc/passwd/``

Deletes line 2, 20 and 25 from myfile.

``sed -i -e '2d;20,25d' ~/myfile``

Change enabled to disabled for lines from 500 to 2000.

``sed -i "-e 500,2000 s/enabled/disabled/g" /home/bob/values.conf``

Change disabled to enabled globally and ignore the case for disabled with the "i" operator. Will switch out "disabled", "Disabled", and "DISABLED" to "enabled."

``sed -i "s/disabled/enabled/gi" /home/bob/values.conf``

Replace all occurrence of string #%$2jh//238720//31223 with $2//23872031223 in "/home/bob/data.txt" file.

``sed -i 's~#%$2jh//238720//31223~$2//23872031223~g' /home/bob/data.txt``

## Other commands

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