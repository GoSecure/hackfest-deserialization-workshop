# Exercise 4 - Building a gadget and exploiting a service

Source code (same as exercise 3): 
https://github.com/GoSecure/goinsecure-deserialization

Recommended IDE: https://www.jetbrains.com/idea/

Target: POST http://httpwn.com:8002/uploadBackup

# Modifying the code to build the gadget

Refer to the slide deck pages : 34 to 45.

# HTTP Request

The HTTP request should look like:

```
POST /uploadBackup HTTP/1.1
Host: httpwn.com:8002
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:57.0) Gecko/20100101 Firefox/57.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Connection: close
Upgrade-Insecure-Requests: 1
Content-Type: application/x-www-form-urlencoded
Content-Length: 627

backup=[PAYLOAD]
```