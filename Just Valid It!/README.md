I use ExeinfoPE to check the EXE and i found out it’s packed using ConfuserEX 1.0. Using de4dot with no success. Later that I found an unpacker on github and i use it to unpack the exe.
The next step is view the code in dnspy and i see this

```
string passPhrase = "This is not the fl4g";
string saltValue = "g$r4mK4$aR";
string hashAlgorithm = "SHA1";
int passwordIterations = 1337;
string initVector = "wargamesmynanosx";
int keySize = 256;
WebResponse response = WebRequest.Create(new Uri("https://janganhackstorbarangpls.wargames.my/f85ee8d101fce12a750377804bfe76be6b8753b225a72e73b0167200")).GetResponse();
Console.WriteLine(((HttpWebResponse)response).StatusDescription);
string arg = Program.Decrypt(new StreamReader(response.GetResponseStream()).ReadToEnd(), passPhrase, saltValue, hashAlgorithm, passwordIterations, initVector, keySize);
Console.WriteLine("ACCEPTED!\n");
Console.WriteLine(string.Format("Flag : {0}", arg));
Console.ReadKey();
```

So here we go we just need to paste the code in visual studio (remember to copy function Decrypt too) and run the code and we got the flag.

![flag](https://github.com/kaizensecurity/WGMY2018/blob/master/Just%20Valid%20It!/flag.jpg)
```
flag : wgmy{is_1t_DLL_1nJ3ct10n?}
```
