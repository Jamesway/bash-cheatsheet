# Bash Cheatsheet
http://wiki.bash-hackers.org/commands/classictest

## Keep Variables in Braces  
braces {} prevent unwanted variable expansion
```
foo="foo"
foobar="baz"

echo $foo #foo
echo $foobar #baz, but maybe we wanted "foobar"

echo ${foo}bar #foobar
```

## Conditionals  
conditional expression in brackets [], followed by a "then" and ended with a "fi"
```
# notice the semicolon
if [ condition ]
then
  echo "hi"
else
  echo "hello"
fi
```

### check if a file exists ( -f )
```
if [ -f $file ]
then
  echo "file exists"
fi
```

### check if parameter exists ( -n )
```
if [ -n "$1" ]
then
  echo "parameter 1 is ${1}"
fi
```

### check if parameter doesn't exist ( -z )
```
if [ -z "$1" ]
then
  echo "no parameter 1"
fi
```

### equality ( = / != )
single "=" tests equality unlike most languages where "==" tests equality and single "=" assigns, bash tests with singe "="  
"!=" still tests for inequality
```
var1="abc"
var2="xyz"
if [ $var = $var2 ]
then
  echo "they're equal"
fi

if [ $var1 != $var2 ]
then
  echo "they're not equal"
fi
```

### and/or
```
if [ -n "${VAR1}" ] && [ "${VAR1}" = "${VAR2}" ]
then
  ...
fi

if [ -z "${VAR1}" ] || [ "${VAR1}" != "${VAR2}" ]
then
  ...
fi
```

## For Loops
for loop logic is followed by a "do" and ended with a "done"
### for in ( a la python)
```
for i in ${FILES}
do
  ...
done

for i in {1...10}
do
  echo i
done

for i in 1 2 3 4 5
do
  echo i
done
```

### c style for loop
uses double parentheses
```
for (( i=0; i<10; i++ ))
do
  echo i
done
```


## Text Manipulation
### trim characters
https://stackoverflow.com/a/45822753
http://mywiki.wooledge.org/BashFAQ/100#Removing_part_of_a_string
```
# trim a whitespace from end
${MYVAR%" "}

# trim all whitespace from end
${MYVAR%%" "}

$APP_PATH=/path/to/my/app

# remove the first directory
${APP_PATH#/path}
```

### remove spaces with translate ( tr )
```
STRING="this is a string with spaces"
echo $(STRING) | tr -d [:space:]
```

### find a line in a file with grep
```
SETTINGS_FILE="settings.py"

grep SECRET_KEY | ${SETTINGS_FILE}
```

### replace strings in a file with sed
```
# -i does an inline replace - you can specify a backup file or not
# single quotes are necessary to prevent bash from intepreting special characters
sed -i "s/REGEX/REPLACEMENT/" ${SUBJECT_FILE}
```

## Command Line Parameters

### all parameters
```
$@
```

### the running script
```
$0
```

### 1st, 2nd, nth parameter
```
$1...n
```
