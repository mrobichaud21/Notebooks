## Print Output
Cmd | awk -F ' ' {'print $1’}

EG:
kubectl get namespaces | awk -F ' ' {'print $1'}

## Execute command
cmd | awk -f ' ' '{system("cmd " $1 }'
EG:
oc get dc --no-headers | awk -F ' ' '{system("oc delete dc " $1 )}'
oc get pods --no-headers --no-headers | awk -F ' ' '{system("oc logs " $1 " >> tmp.log")}'
oc get dc --no-headers | awk -F ' ' '{system("oc set env --list dc " $1 " | grep SPRING_PROFILES_ACTIVE ")}'

## using substr and length
oc get secrets | grep helm.sh/release.v1 | awk -F ' ' {'print substr($1,0,length($1)-3)'} | sort --unique


AWK has the following built-in String functions −
asort(arr [, d [, how] ])

This function sorts the contents of arr using GAWK's normal rules for comparing values, and replaces the indexes of the sorted values arr with sequential integers starting with 1.

Example

[jerry]$ awk 'BEGIN { arr[0] = "Three" arr[1] = "One" arr[2] = "Two" print "Array elements before sorting:" for (i in arr) { print arr[i] } asort(arr) print "Array elements after sorting:" for (i in arr) { print arr[i] }}'
On executing this code, you get the following result −

Output

Array elements before sorting:ThreeOneTwoArray elements after sorting:OneThreeTwo
asorti(arr [, d [, how] ])


The behavior of this function is the same as that of asort(), except that the array indexes are used for sorting.

Example

[jerry]$ awk 'BEGIN { arr["Two"] = 1 arr["One"] = 2 arr["Three"] = 3 asorti(arr) print "Array indices after sorting:" for (i in arr) { print arr[i] }}'
On executing this code, you get the following result −

Output

Array indices after sorting:OneThreeTwo
gsub(regex, sub, string)


gsub stands for global substitution. It replaces every occurrence of regex with the given string (sub). The third parameter is optional. If it is omitted, then $0 is used.

Example

[jerry]$ awk 'BEGIN { str = "Hello, World" print "String before replacement = " str gsub("World", "Jerry", str) print "String after replacement = " str}'
On executing this code, you get the following result −

Output

String before replacement = Hello, WorldString after replacement = Hello, Jerry
index(str, sub)


It checks whether sub is a substring of str or not. On success, it returns the position where sub starts; otherwise it returns 0. The first character of str is at position 1.

Example

[jerry]$ awk 'BEGIN { str = "One Two Three" subs = "Two" ret = index(str, subs) printf "Substring \"%s\" found at %d location.\n", subs, ret}'
On executing this code, you get the following result −

Output

Substring "Two" found at 5 location.
length(str)


It returns the length of a string.

Example

[jerry]$ awk 'BEGIN { str = "Hello, World !!!" print "Length = ", length(str)}'
On executing this code, you get the following result −

Length = 16
match(str, regex)


It returns the index of the first longest match of regex in string str. It returns 0 if no match found.

Example

[jerry]$ awk 'BEGIN { str = "One Two Three" subs = "Two" ret = match(str, subs) printf "Substring \"%s\" found at %d location.\n", subs, ret}'
On executing this code, you get the following result −

Output

Substring "Two" found at 5 location
split(str, arr, regex)


This function splits the string str into fields by regular expression regex and the fields are loaded into the array arr. If regex is omitted, then FS is used.

Example

[jerry]$ awk 'BEGIN { str = "One,Two,Three,Four" split(str, arr, ",") print "Array contains following values" for (i in arr) { print arr[i] }}'
On executing this code, you get the following result −

Output

Array contains following valuesOneTwoThreeFour
printf(format, expr-list)


This function returns a string constructed from expr-list according to format.

Example

[jerry]$ awk 'BEGIN { param = 1024.0 result = sqrt(param) printf "sqrt(%f) = %f\n", param, result}'
On executing this code, you get the following result −

Output

sqrt(1024.000000) = 32.000000
strtonum(str)


This function examines str and return its numeric value. If str begins with a leading 0, it is treated as an octal number. If str begins with a leading 0x or 0X, it is taken as a hexadecimal number. Otherwise, assume it is a decimal number.

Example

[jerry]$ awk 'BEGIN { print "Decimal num = " strtonum("123") print "Octal num = " strtonum("0123") print "Hexadecimal num = " strtonum("0x123")}'
On executing this code, you get the following result −

Output

Decimal num = 123Octal num = 83Hexadecimal num = 291
sub(regex, sub, string)


This function performs a single substitution. It replaces the first occurrence of the regex pattern with the given string (sub). The third parameter is optional. If it is omitted, $0 is used.

Example

[jerry]$ awk 'BEGIN { str = "Hello, World" print "String before replacement = " str sub("World", "Jerry", str) print "String after replacement = " str}'
On executing this code, you get the following result −

Output

String before replacement = Hello, WorldString after replacement = Hello, Jerry
substr(str, start, l)


This function returns the substring of string str, starting at index start of length l. If length is omitted, the suffix of str starting at index start is returned.

Example

[jerry]$ awk 'BEGIN { str = "Hello, World !!!" subs = substr(str, 1, 5) print "Substring = " subs}'
On executing this code, you get the following result −

Output

Substring = Hello
tolower(str)


This function returns a copy of string str with all upper-case characters converted to lower-case.

Example

[jerry]$ awk 'BEGIN { str = "HELLO, WORLD !!!" print "Lowercase string = " tolower(str)}'
On executing this code, you get the following result −

Output

Lowercase string = hello, world !!!
toupper(str)


This function returns a copy of string str with all lower-case characters converted to upper case.

Example

[jerry]$ awk 'BEGIN { str = "hello, world !!!" print "Uppercase string = " toupper(str)}'
On executing this code, you get the following result −

Output

Uppercase string = HELLO, WORLD !!!
awk_built_in_functions.htm