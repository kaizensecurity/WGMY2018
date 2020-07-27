At first i had a difficult time solving this challenge due to function blacklist. Since this is PHP challenge. I then try to look into scandir

First attempt
![flag](https://github.com/kaizensecurity/WGMY2018/blob/master/PHP%20Sandbox/sscn.png)

I managed to bypass the blacklist. but this is not our main objective. We want to get the flag. After messing around with it, i noticed that we can use finfo to with scandir to get the flag.
![flag](https://github.com/kaizensecurity/WGMY2018/blob/master/PHP%20Sandbox/fin.png)
```
flag: wgmy{func_bl4ck1ist_1z_s0_b4d}
```
