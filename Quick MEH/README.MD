First we check exe in exeinfope and we found no packer. Then we run the exe and see the text “quickmeh.exe flag ”

Then we open exe in x64dbg and search the string and found is in sub E61000.
First we see it check the flag have 24 character and we know that that the flag format is “wgmy{}” so we need to find 18 character remain.
So the flag is something like this wgmy{xxxxxxxxxxxxxxxxxx}
And the checking loop is like this:

```
mov bl,byte ptr ds:[esi+edx]
mov al,bl
sar al,4
movsx eax,al
movd xmm0,eax
cvtdq2pd xmm0,xmm0
mulsd xmm0,xmm1
ucomisd xmm0,qword ptr ds:[ecx]
lahf 
test ah,44 //1
jp quick.11010A9
and bl,F
movzx eax,bl
movd xmm0,eax
cvtdq2pd xmm0,xmm0
mulsd xmm0,xmm1
ucomisd xmm0,qword ptr ds:[ecx+8]
lahf 
test ah,44 //2
jp quick.11010A9
inc edx
add ecx,10
cmp edx,18
jl quick.1101060
mov bh,1
mov ecx,quick.1102124
```
So we set the breakpoint at //1 and //2 and we run the app and see esi+edx*1:”wgmy{{xxxxxxxxxxxxxxxxxx}}” is change after each loop.

Like this : “wgmy{{xxxxxxxxxxxxxxxxxx}}” -> “gmy{{xxxxxxxxxxxxxxxxxx}}” -> “my{{xxxxxxxxxxxxxxxxxx}}” then we reach “xxxxxxxxxxxxxxxxxx}}”
So we stop at there and saw that the jp quick.11010A9 [jump is taken] so we know x is the wrong character.

Then we re run again using different one like wgmy{axxxxxxxxxxxxxxxxx},wgmy{bxxxxxxxxxxxxxxxxx},…. all of them is trigger the jmp again so all wrong then we reach wgmy{ixxxxxxxxxxxxxxxxx} the jmp is not taken so we got the first one!

So after the bruteforce process we got the flag: 

```
wgmy{is-it_m3th-0r_M4th}
```
