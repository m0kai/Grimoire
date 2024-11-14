-- -
### Password Mutations
Create custom password lists by taking in a list of words and mutating them into possible combinations of that word, i.e. input `password` then mutate it to include `Password123` and `p@ssw0rd`. Rule files have syntax such as the following:

|**Function**|**Description**|
|---|---|
|`:`|Do nothing.|
|`l`|Lowercase all letters.|
|`u`|Uppercase all letters.|
|`c`|Capitalize the first letter and lowercase others.|
|`sXY`|Replace all instances of X with Y.|
|`$!`|Add the exclamation character at the end.|

Example File `custom.rule` could look something like:
```
:
c
so0
c so0
sa@
c sa@
c sa@ so0
$!
$! c
$! so0
$! sa@
$! c so0
$! c sa@
$! so0 sa@
$! c so0 sa@
```
And then you would generate a custom file with:
```bash
hashcat --force password.lst -r custom.rule --stdout | sort -u > mut_password.lst
```
*Note: a good bultin rule to use is* `/usr/share/hashcat/rules/best64.rule`