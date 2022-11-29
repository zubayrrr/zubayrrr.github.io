---
created: 1652946820003
desc: ''
id: 26fd6bw5fsykdus523f40bz
title: Bash
updated: 1661687805687
---
   
Bash is a Unix shell and command language written by Brian Fox for the GNU Project as a free software replacement for the Bourne shell. First released in 1989, it has been used as the default login shell for most Linux distributions. Bash was one of the first programs [Linus Torvalds](/not_created.md) ported to Linux, alongside GCC.   
   
## Bash Aliases   
   
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
   
- Aliases for commands   
- Nicknames for your pipelines   
- To get started you need a file in your user's `Home` dir named `.bash_aliases`   
- Write the command inside the `.bash_aliases` file after writing `alias aliasName='command1 -opt args | command2 -opt args ...'` or alias for command that don't accept [Redirecting stdin & stderr](../devlog/redirecting%20stdin%20%26%20stderr.md) can be acheived by `alias aliasName='xargs command -opt args...'`   
- Example:   
   
`alias getdates='date | tee /home/user/date.txt | cut -d " " -f 1 | tee /home/user/day.txt | xargs echo hello'`   
   
   
- You can also build piplines using multiple aliases, the first command in an alias should accept [Redirecting stdin & stderr](../devlog/redirecting%20stdin%20%26%20stderr.md)   
- Terminal will have to be rebooted after creating an alias.   
   
## List all aliases   
   
```bash
alias
```
   
   
## Escape an alias / run the original command   
   
Use `\` to escape an alias   
   
```bash
\ls
```
   
   
## Create an alias   
   
This will create an alias for the existing session. To make aliases persist in all of your user session, create them inside in your `~/.zshrc`, `~/.bashrc`, `~/.bash_profile` (and reload the shell or run `source ~/.zshrc`).   
   
```bash
alias ls="ls -ltr"
```
   
   
## Remove an alias   
   
```bash
unalias ls
```

   
   
   
---   
   
## Introduction   
   
   
- To check what shell was started use `echo $0`   
- List all installed shells `cat /etc/shells`   
- Check each user's default shell `cat /etc/passwd` last column   
   
A shell script is an executable text file that contains commands, variables, functions, loops and so on that are executed sequentially.   
   
It is widely used for automating repetitive tasks, customize administrative tasks, create your own powertools or small applications. Other examples of scripting can be found in: monitoring the system, data backup/restore, email based alert system, security auditing.   
   
## The Shebang   
   
The Shebang is made of `#!` is followed by the path of the interpreter.   
   
`#!/bin/bash`   
   
For executable scripts the system expects The Shebang in the first line of the script that indicates which program to run as the interpreter with the script file as the argument.   
Basically, to indicate what program will run the file whether bash, python, php or other interpreters.   
   
If you execute a script without the shebang the interpreter will use the default shell.   
   
Run `which bash` `which -a bash` to find the location of the interpreter.   
   
When using Python as the interpreter for a script   
   
`#!/usr/bin/python3` will be the first line of the script(with the python code)   
   
## Comments   
   
Bash will ignore everything written after the `#` symbol. The only exception being The Shebang   
Bash doesn't support multi line commenting. See [here document](../devlog/here%20document.md)   
   
## Running Bash Scripts   
   
   
- Make it executable   
  - `chmod +x script.sh`   
- Run it with its relative path using `./script.sh`   
- Or run it with its absolute path   
   
   
  - The script will run in a sub shell   
   
   
- You can also pass the name of the interpreter before the script(this will make the script work even if you don't explicity give it execution permission) such as:   
   
   
  - `bash script.sh`   
  - `python3 script.py`   
   
   
- `source script.sh` or `. script.sh`   
  - Will make the script run in the current shell.   
   
## Variables   
   
Variable is a name of a memory location where a value which can be manipulated is stored.   
   
   
- `foo=bar` space before and after `=` assignment operator is not allowed.   
- If the value of the variable is a string that contains spaces, enclose it with `" "` double quotes.   
- Bash is a weakly typed langauge and doesn't require you to define any data type at variable declaration.   
- There are no floating point numbers in bash. Only integers.   
- Variable names cannot start with a number nor can they have special characters in them.   
- It can contain an underscore or different case.   
- Giving a value to a variable is called assigning variable a value.   
- Retrieving a value stored in a variable is called referencing.   
- Preceed a variable with `$` to access it's value.   
- Variable name is not referenced if single quotes are used (such as in an echo statement).   
- Use backslash to escape a reserved character's role such as `\$PATH`.   
- A variable can reference value from an existing variable `newVar="$oldVar"`   
   
Use `set` command to retrieve value to get all shell variables and functions.   
   
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
   
- They're defined for the current shell and are inherited by any child shells or processes.   
- They're used to pass information to process that are spawned from the current shell.   
- Displayed using `env` or `printenv`   
- [path](/not_created.md) is such an example   
- When assigning multiple values to a variable, its common to separate them using a colon `:`   
- By convention - env variables are written in uppercase letters.   
- Usually they're not used directly; instead they're referenced by individual applications/services.   
  - `$HOME` is such an example   
- Run `env | less` to list all env variable set on your machine.   
- You can also use `printenv` to print variables   
  - `printenv SHELL PWD LC_TIME`   
   
## Create a new env variable   
   
   
- Add a line: `export VARNAME=VARVAL` in your `~/.zshrc`   
- To create a system wide variable available for all users; declare the variable in `/etc/profile` or `/etc/bash.bashrc`   
- There is also `/etc/environment` in which you can set env variables each on a new line
   
   
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
   
- They're contained exclusively within the shell in which they were set or defined.   
- Displayed using `set`   
- Running `set` command will display shell functions as well as to display all available variables.   
- To display only shell and [environment variable](../devlog/environment%20variable.md) - specify set to operate in [POSIX](../devlog/posix.md) mode   
  - `set -o posix`
   
   
## Constants   
   
Declare constants(variables whose values doesn't change) using `declare -r constName="constVal"`   
   
You cannnot `unset` or delete a read-only variable.   
   
## Create Your First Bash Script   
   
1. `vim first_script.sh`   
   
   - some people consider giving extensions to an executable as a bad practice.   
2. complete the script   
   
```bash
mkdir -p new_dir
echo "yay! first script" > new_dir/file.txt
ls -l new_dir
cat new_dir/file.txt
```
   
   
3. Save and exit   
4. Give permissions for execution   
   
`chmod 700 first_script.sh`   
   
5. Execute it using relative path   
   
`./first_script.sh`   
   
If you don't use relative path, shell will throw an error because it would be looking for commands and scripts from the [path](/not_created.md) variable.   
   
## User Input   
   
   
- `read` is responsible for collecting user input - it'll stop a program until the user has given an input and has returned the input with the RETURN or ENTER Key   
   
   
- Create a new variable with some prompt   
   
`read -p "some prompt for user: " $varName`   
   
   
- Create a new variable that doesn't display the input (like entering password)   
   
`read -s -p "safely enter value: " $varName`   
   
## Special Variables and Positional Arguments   
   
Lets take the following command for example   
   
`./script filename1 dir1 10.0.0.1`   
   
There are predefined variables available such:   
   
`$0` is the name of the script itself (`./script.sh`)   
`$1` is the first positional argument (`filename`)   
`$2` is the second positional argument (`dir1`)   
`$3` is the third positional argument (`10.0.0.1`)   
`$9` would be the ninth and after it arguments must be enclosed in `{}` curly braces such as `${10}` for the tenth   
   
`$#` is the number of the positional arguments   
`"$*"` is the string representation of all positional arguments: `$1` `$2` `$3` ...   
`$?` is the most recent foreground command exit status   
   
## If, Elif and Else Statements   
   
```bash
if [some condition is true]
then
    // execute this code
elif [some other condition is true]
then
    // execute this code
else
    // execute this code
fi
```
   
   
## `[]` vs `[[]]`   
   
`[]` is the old way used for testing conditions.   
   
`[[]]` is the new way of testing conditions and is considered to be safer. Double square brackets prevent word splitting or string variables that contain spaces, you don't need to double qoute string variables even though its a good practice. It also have features like [regular expression](../devlog/regular%20expression.md) matching.   
   
## Testing Conditions For Numbers   
   
Run `man test` to list all available testing (comparison operators for integer comparison)   
   
## Multiple Conditions and Nested If Statements   
   
Using local operators allow you to use multiple conditions in the if statement.   
   
`&&` is the AND operator   
`||` is the OR operator   
   
## Command Subsitution   
   
In the following example, the `date` command was executed and the output is stored inside the variable `now`.   
   
```bash
now=`date`
```
   
   
If the output is going to be a string, it is recommended to enclose it inside double quotes.   
   
```bash
now="`date`"
```
   
   
The other way of doing command subsitution is:   
   
```bash
user=`$(who)`

# this is same as:

user="`who`"
```
   
   
You can substitute the entire command line, which can be multiple commands piped together.   
   
`ps -ef | grep bash`   
   
`output="$(ps -ef | grep bash)"`   
   
## Comparing Strings in If Statements   
   
Two strings are equal if their length is same and contains the same sequence of characters in the same order.   
   
   
- The comparsion operator is a single `=` sign when using if statement with `[]` single square brackets and its `==` when using double square brackets `[[]]`   
   
   
- The inequality operator is `!=`   
   
One of the approach to check for substring inside a string is to surround the substring with asterisk `*` to make it match all the characters.   
   
```bash
str1="Linux is amazing"
if [[ "str1" == *"Linux"*]]
```
   
   
   
- `-n` returns true if the string length is NON zero and `-z` returns true if the string length is zero.   
   
## For Loop   
   
```bash
for item in LIST
do
  commands
done
```
   
   
### Examples   
   
```bash
#!/bin/bash

for os in Ubuntu CentOS "MX Linux" Kali Manjaro
do
  echo "os is $os"
done
```
   
   
   
---   
   
```bash
#!/bin/bash
for num in {3..7}
do
  echo "num is $num"
done
```
   
   
   
---   
   
Defining increment for a range   
   
```bash
#!/bin/bash

for num in {10..100..5}
do
  echo "num is $num"
done
```
   
   
   
---   
   
Going through the current directory, displaying the contents of the files   
   
```bash
#!/bin/bash

for item in ./*
do
  if [[ -f "$item" ]]
  then
      echo "Displaying the contents of $item"
      sleep 1
      cat $item
      echo "##########"
  fi
done
```
   
   
   
---   
   
Rename all files in the current directory ending in `.txt` extension by adding a string at the start of the file name   
   
```bash
#!/bin/bash

for file in *.txt
do
  mv "$file" "renamed_$file"
done
```
   
   
### For Loops   
   
```bash
#!/bin/bash

for ((i=0;i<=50;i++))
do
  echo "i = $i"
done
```
   
   
## While Loops   
   
It is used to execute a set of commands as long as the given condition evaluates to true.   
   
```bash
while CONDITION
do
  COMMANDS
done
```
   
   
Use `:` to always return true   
   
```bash
while :
do
  output="$(pgrep -l $1)"
  if [[ -n "$output" ]]
  then
      echo "The process  \"$1"\ is running.
  else
      echo "The process  \"$1"\ is NOT running.
  fi
  sleep 3
done
```
   
   
### Examples   
   
```bash
#!/bin/bash

i=0

while [[ $i -lt 10]]
do
  echo "i: $i"
  ((i++)) # let i = i++
done
```
   
   
## Case Statements   
   
The case construct allows us to test string and numbers and is infact a simpler form of bash if, elif, else statement.   
   
Case is similar to Switch statements in other programming languages.   
   
It is not a loop, it doesn't execute a block of code `n` number of times. Instead, bash shell checks the conditions and controls the flow of the program.   
   
```bash
case EXPRESSION in
  PATTERN_1)
    STATEMENTS
    ;;
  PATTERN_2)
   STATEMENTS
    ;;
  PATTERN_3)
    STATEMENTS
    ;;
  PATTERN_N)
    STATEMENTS
    ;;
    *)
    STATEMENTS
    ;;
esac
```
   
   
### Examples   
   
```bash
#!/bin/bash

echo -n "Enter your favourite pet: "
read PET

case "$PET" in
    dog)
        echo "Your favourite pet is dog"
        ;;
    cat||CAT)
        echo "You like cats"
        ;;
    fist||"African turtle")
        echo "Fish or turtles are great"
        ;;
    *)
        echo "Your favourite pet is unknown"
esac
```
   
   
   
---   
   
```bash
#!/bin/bash

if [[ $# -ne 2 ]]
then
    echo "Run the script with 2 arguments: Signal and PID"
    exit
fi
case "$1" in
      1)
        echo "Sending the SIGHUP signal to $2"
        kill -SIGHUP $2
        ;;
      2)
        echo "Sending the SIGINT signal to $2"
        kill -SIGINT $2
        ;;
      15)
        echo "Sending the SIGTERM signal to $2"
        kill -15 $2
        ;;
      *)
        echo "Signal number $1 will not be delivered"
        ;;
esac
```
   
   
## Functions   
   
There are two different formats for declaring a function.   
   
```bash
#!/bin/bash

function print_something () {
  echo "I am a function"
}
```
   
   
```bash
display_something () {
  echo "Hello world!"
}
```
   
   
To call a function just write it's name without any paranethesis `display_something`   
   
### Arguments   
   
In bash you cannot pass arguments through the paranthesis, they're only for decoration.   
To pass any information to the function use arguments like they're passed to a command.   
   
```bash
#!/bin/bash

create_files () {
  echo "Creating $1"
  touch $1
  chmod 400 $1
  echo "Creating $2"
  touch $2
  chmod 600 $2
}

create_files file1.txt file2.txt
```
   
   
### Returns   
   
Bash doesn't allow you to return a value of a function, doing so using the return keyword, we're setting the status of the command executed or of the function. $? contains the status of previously run command or function.   
   
Typically, a value of `0` means everything went successfully and a non zero value means something did not went succesfully.   
   
```bash
#!/bin/bash

create_files () {
  echo "Creating $1"
  touch $1
  chmod 400 $1
  return 10
}

create_files file1.txt
```
   
   
To get a real "return" value like in other programming languages, you can try command substitution.   
   
```bash
#!/bin/bash

function lines_in_file () {
  grep -c "$1" "$2"
}

n=$(lines_in_file "usb" "/var/log/dmesg")
echo $n
```
   
   
## Variable Scope in Functions   
   
Scope refers to which part of a script the variable is "visible". In bash, all variables by default are global; they're visible everywhere inside a script.   
   
If you want to define a local variable within the function body, use the `local` keyword before declaring variable.   
It is considered a good practice to use local variables in order to contain everything inside a function.   
   
```bash
#!/bin/bash

var1="AA"
var2="BB"

function func1 () {
  var1="XX"
  local var2="YY"
  echo "Inside func1: var1=$var1 and var2=v$var2"
}
func1
echo "After calling func1: var1=$var1 and var2=v$var2"
```
   
   
## Select   
   
```bash
select ITEM in LIST
do
  commands
done
```
   
   
   
- ITEM is a user defined variable and the LIST is a series of strings, numbers or output of commands.   
   
```bash
#!/bin/bash

select COUNTRY in Germany India "United Kingdom"
do
  echo "Country is $COUNTRY"
  echo "Your choice is $REPLY"
done
```
   
   
Use `PS3` to define a prompt   
   
```bash
#!/bin/bash

PS3="Choose your country: "
select COUNTRY in Germany India "United Kingdom"
do
  echo "Country is $COUNTRY"
  echo "Your choice is $REPLY"
done
```
   
   
   
- You can use `select` with `case` and `if` statements   
   
## Examples   
   
   
- [connection testing](../devlog/connection%20testing.md)   
- [Dropping a List of IP addresses Using a For Loop](../devlog/dropping%20a%20list%20of%20ip%20addresses%20using%20a%20for%20loop.md)   
- [System Administration Script using Menus](../devlog/system%20administration%20script%20using%20menus.md)   
   
## Resources   
   
   
- [Developing Console Applications with Bash | Linux Journal](https://www.linuxjournal.com/content/developing-console-applications-bash)