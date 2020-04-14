
## she-bang
`#!/usr/bin/env bash'`

## Check for null || not null
### Process if not null
`if [ -n "${SECRET_PARAPHASE}" ]; then
      blah blah
fi`

### Process if null
`if [ -z ${PORT_DATA} ]; then
      blah blah
fi`

## String or Array Length
Str=abcdefghjecho
"Str is: ${#Str} "characters long"

## Substring
#!/bin/bash
v="some string.rtf"
v2=${v::-4}
echo "$v --> $v2"

https://stackoverflow.com/questions/27658675/how-to-remove-last-n-characters-from-a-string-in-bash


## case statement

https://linuxize.com/post/bash-case-statement/