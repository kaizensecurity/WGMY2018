Who else love ~meth?~ math..This question is quite straight forward, no bullshit. You just need brain & python basic to solve this.

So this is the python code were used during the challenge

```
#!/usr/bin/python
 
from pwn import *
 
def math_scientist(quiz):
    if 'x' in quiz:
        answer = quiz.replace('x', '*')
        return str(eval(answer))
    else:
        return str(eval(quiz))
 
r = remote('206.189.93.101', 4343)
 
r.recvuntil('> ')
r.sendline("start")
i = 0
while i  '))
    print tmp
    pos = tmp.index(']')+2
    # quiz = tmp[pos:pos+7].replace("\\","")
    quiz = tmp[pos:pos+7]
    r.sendline(math_scientist(quiz.split(';')[0]))
    i += 1
print r.read()
```

```
 wgmy{d0_you_ev3n_m4th_br0}
```
