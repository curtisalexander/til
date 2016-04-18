# Shell Scripting Cheatsheet

## Variables

Courtesty http://stackoverflow.com/a/5163260.

```sh
$1, $2, ...	are the positional parameters
"$@" 		is an array-like construct of all positional parameters, {$1, $2, ...}
"$*" 		is the IFS expansion of all positional parameters, $1 $2 ...
$# 			is the number of positional parameters
$- 			current options set for the shell
$$ 			pid of the current shell (not subshell)
$_ 			most recent parameter (or the abs path of the command to start the current shell immediately after startup)
$IFS 		is the (input) field separator
$? 			is the most recent foreground pipeline exit status
$! 			is the PID of the most recent background command
$0 			is the name of the shell or shell script
```

## Logic

Summary of shell (`bash` or `zsh`) logic.

```sh
-d      	true if directory exists
-e          true if file exists
-f          true if file exists and is a regular file
-h          true if file exists and is a symbolic link
-n          true if the length of string is non-zero
-o          true if the shell option is enabled
-z			true if the length of the string is zero
```

## Comparisons

Comparisons between strings vs integers.

```sh
# strings
string1 == string2
string1 != string2
string1 < string2   # lexicographic sorting
string1 > string2   # lexicographic sorting

# integers
arg1 -eq arg2
arg1 -ne arg2
arg1 -lt arg2
arg1 -le arg2
arg1 -gt arg2
arg1 -ge arg2
```

## Further Reading
See the [Bash FAQ](http://mywiki.wooledge.org/BashFAQ/031) for a difference between `[` and `[[`.
