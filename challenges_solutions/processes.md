# Processes exercises

## ex 29
```
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/wait.h>

void pwncollege(void) {
        pid_t my_pid;
        int status, timeout;

        char **argv = calloc(5, sizeof(char*));
        argv[0] = "challenge_path";

        if ((my_pid = fork()) == 0) {
                execve(argv[0], (char **)argv, NULL);
        }

        timeout = 1000;
        while ((waitpid(my_pid, &status, WNOHANG) == 0)) {
                if (--timeout < 0) {
                        perror("timeout");
                        //return -1;
                }
                sleep(1);
        }

}

int main(void) {
        pwncollege();
        return 0;
}
```

## ex 30
same as 29

## ex 31
same as 29 but with
```
argv[1] = "password";
```

## ex 32
same as 29 but with
```
char **envp = calloc(5, sizeof(char*));
envp[0] = "hxaavp=qtsnmtxmsl";

        if ((my_pid = fork()) == 0) {
                execve(argv[0], (char **)argv, (char **)envp);
        }
```

## ex 33
same as 29

## ex 34
same as 29

## ex 35
same as 29 but executed with
```
env --ignore-environment
```

## ex 36
- the challenge checks for a specific parent process : bash
- the challenge checks for a specific process at the other end of stdout : cat

```
/challenge/level | cat
```

## ex 37
- the challenge checks for a specific parent process : bash
- the challenge checks for a specific process at the other end of stdout : grep
```
/challenge/level | grep flag_prefix
```

## ex 38
- the challenge checks for a specific parent process : bash
- the challenge checks for a specific process at the other end of stdout : sed  
```
/challenge/level | sed l
```

## ex 39
- the challenge checks for a specific parent process : bash
- the challenge checks for a specific process at the other end of stdout : rev
```
/challenge/level | rev | rev
```

## ex 40
- the challenge checks for a specific parent process : bash
- the challenge checks for a specific process at the other end of stdin : cat
- the challenge will check for a hardcoded password over stdin : password
```
cat - | /challenge/level
```

## ex 41
- the challenge checks for a specific parent process : bash
- the challenge checks for a specific process at the other end of stdin : rev
- the challenge will check for a hardcoded password over stdin : password
```
rev | /challenge/level
```
then write the password reversed

## ex 42
- the challenge checks for a specific parent process : shellscript
- the challenge checks for a specific process at the other end of stdout : cat
```
#! /usr/bin/bash

var=`/challenge/level | cat`
echo $var
```

## ex 43
- the challenge checks for a specific parent process : shellscript
- the challenge checks for a specific process at the other end of stdout : grep
```
#! /usr/bin/bash

var=`/challenge/level | grep flag_prefix`
echo $var
```

## ex 44
- the challenge checks for a specific parent process : shellscript
- the challenge checks for a specific process at the other end of stdout : sed
```
#! /usr/bin/bash

var=`/challenge/level | sed l`
echo $var
```

## ex 45
- the challenge checks for a specific parent process : shellscript
- the challenge checks for a specific process at the other end of stdout : rev
```
#! /usr/bin/bash

var=`/challenge/level| rev | rev`
echo $var
```

## ex 46
- the challenge checks for a specific parent process : shellscript
- the challenge checks for a specific process at the other end of stdin : cat
- the challenge will check for a hardcoded password over stdin : password
```
#! /usr/bin/bash

var=`cat - | /challenge/level`
echo $var
```

## ex 47
- the challenge checks for a specific parent process : shellscript
- the challenge checks for a specific process at the other end of stdin : rev
- the challenge will check for a hardcoded password over stdin : password
```
#! /usr/bin/bash

var=`rev | /challenge/level`
echo $var
```

## ex 48
- the challenge checks for a specific parent process : ipython
- the challenge checks for a specific process at the other end of stdout : cat
```
ipython
import subprocess
p1 = subprocess.Popen(["/challenge/level"], stdout=subprocess.PIPE)
p2 = subprocess.run(["/bin/cat"], stdin=p1.stdout)
```

## ex 49
- the challenge checks for a specific parent process : ipython
- the challenge checks for a specific process at the other end of stdout : grep
```
ipython
import subprocess
p1 = subprocess.Popen(["/challenge/level"], stdout=subprocess.PIPE)
p2 = subprocess.run(["/bin/grep", "flag_prefix"], stdin=p1.stdout)
```

## ex 50
- the challenge checks for a specific parent process : ipython
- the challenge checks for a specific process at the other end of stdout : sed
```
ipython
import subprocess
p1 = subprocess.Popen(["/challenge/level"], stdout=subprocess.PIPE)
p2 = subprocess.run(["/bin/sed", "l"], stdin=p1.stdout)
```

## ex 51
- the challenge checks for a specific parent process : ipython
- the challenge checks for a specific process at the other end of stdout : rev
```
ipython
import subprocess
p1 = subprocess.Popen(["/challenge/level"], stdout=subprocess.PIPE)
p2 = subprocess.Popen(["/bin/rev"], stdin=p1.stdout, stdout=subprocess.PIPE)
p3 = subprocess.run(["/bin/rev"], stdin=p2.stdout)
```

## ex 52
- the challenge checks for a specific parent process : ipython
- the challenge checks for a specific process at the other end of stdin : cat
- the challenge will check for a hardcoded password over stdin : password  
```
ipython
import subprocess
p1 = subprocess.Popen(["/bin/cat", "input.txt"], stdout=subprocess.PIPE) # in input repeat password many times
p2 = subprocess.run(["/challenge/level"], stdin=p1.stdout)
```

## ex 53
- the challenge checks for a specific parent process : ipython
- the challenge checks for a specific process at the other end of stdin : rev
- the challenge will check for a hardcoded password over stdin : password  
```
ipython
import subprocess
p1 = subprocess.Popen(["/bin/rev", "input.txt"], stdout=subprocess.PIPE) # in input repeat password inverted many times
p2 = subprocess.run(["/challenge/level"], stdin=p1.stdout)
```

## ex 54
- the challenge checks for a specific parent process : python
- the challenge checks for a specific process at the other end of stdout : cat
```
import subprocess
p1 = subprocess.Popen(["/challenge/level"], stdout=subprocess.PIPE)
p2 = subprocess.run(["/bin/cat"], stdin=p1.stdout)
```

## ex 55
- the challenge checks for a specific parent process : python
- the challenge checks for a specific process at the other end of stdout : grep
```
import subprocess
p1 = subprocess.Popen(["/challenge/embryoio_level55"], stdout=subprocess.PIPE)
p2 = subprocess.run(["/bin/grep", "flag_prefix"], stdin=p1.stdout)
```

## ex 56
- the challenge checks for a specific parent process : python
- the challenge checks for a specific process at the other end of stdout : sed  
```
import subprocess
p1 = subprocess.Popen(["/challenge/embryoio_level56"], stdout=subprocess.PIPE)
p2 = subprocess.run(["/bin/sed", "l"], stdin=p1.stdout)
```

## ex 57
- the challenge checks for a specific parent process : python
- the challenge checks for a specific process at the other end of stdout : rev
```
import subprocess
p1 = subprocess.Popen(["/challenge/level"], stdout=subprocess.PIPE)
p2 = subprocess.Popen(["/bin/rev"], stdin=p1.stdout, stdout=subprocess.PIPE)
p3 = subprocess.run(["/bin/rev"], stdin=p2.stdout)
```

## ex 58
- the challenge checks for a specific parent process : python
- the challenge checks for a specific process at the other end of stdin : cat
- the challenge will check for a hardcoded password over stdin : password
```
import subprocess
p1 = subprocess.Popen(["/bin/cat"], stdout=subprocess.PIPE)
p2 = subprocess.run(["/challenge/level"], stdin=p1.stdout)
```

## ex 59
- the challenge checks for a specific parent process : python
- the challenge checks for a specific process at the other end of stdin : rev
- the challenge will check for a hardcoded password over stdin : password
```
import subprocess
p1 = subprocess.Popen(["/bin/rev"], stdout=subprocess.PIPE)
p2 = subprocess.run(["/challenge/level"], stdin=p1.stdout)
```

## ex 60
- the challenge checks for a specific parent process : binary
- the challenge checks for a specific process at the other end of stdout : cat
same as 29 but:  
```
./es | cat
```

## ex 61
- the challenge checks for a specific parent process : binary
- the challenge checks for a specific process at the other end of stdout : grep  
same as 29 but:  
```
./es | grep flag_prefix
```

## ex 62
- the challenge checks for a specific parent process : binary
- the challenge checks for a specific process at the other end of stdout : sed  
same as 29 but:  
```
./es | sed l
```

## ex 63
- the challenge checks for a specific parent process : binary
- the challenge checks for a specific process at the other end of stdout : rev  
same as 29 but:  
```
./es | rev | rev
```

## ex 64
- the challenge checks for a specific parent process : binary
- the challenge checks for a specific process at the other end of stdin : cat
- the challenge will check for a hardcoded password over stdin : password  
same as 29 but:  
```
echo password > input.txt
cat input.txt | ./es
```

## ex 65
- the challenge checks for a specific parent process : binary
- the challenge checks for a specific process at the other end of stdin : rev
- the challenge will check for a hardcoded password over stdin : password
same as 29 but:  
```
echo inverted_password > input.txt
rev input.txt | ./es
```

## ex 66
- the challenge checks for a specific parent process : find
```
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/wait.h>

void pwncollege(void) {
  char **argv1 = calloc(5, sizeof(char*));
  argv1[0] = "/challenge/level";

  char **argv2 = calloc(5, sizeof(char*));
  argv2[0] = "/bin/find";
 
  pid_t pid = fork();
 
  if (pid == 0) { // in child process
    execve(argv1[0], (char **)argv1, NULL); //***
  }
 
  if (pid > 0) { // in main process
    wait(NULL);
    execve(argv2[0], (char **)argv2, NULL); //***
  }
 
}

int main(void) {
    pwncollege();
    return 0;
}
```

## ex 67
- the challenge checks for a specific parent process : find
- the challenge will check that argv[NUM] holds value VALUE (listed to the right as NUM:VALUE) : 1:value
same as 67 but with
```
// inside level execve 
argv1[1] = "value";
```

## ex 68
- the challenge checks for a specific parent process : shellscript
- the challenge will check that argv[NUM] holds value VALUE (listed to the right as NUM:VALUE) : 172:value
```
var=`/challenge/level ... ... ... value`
echo $var
```

## ex 70
- the challenge checks for a specific parent process : shellscript
- the challenge will check that the environment is empty (except LC_CTYPE, which is impossible to get rid of in some cases)
- the challenge will check that env[KEY] holds value VALUE (listed to the right as KEY:VALUE) : 325:value  
```
var=`env -i 325=value /challenge/level`
echo $var
```

## ex 71
- the challenge checks for a specific parent process : shellscript
- the challenge will check that the environment is empty (except LC_CTYPE, which is impossible to get rid of in some cases)
- the challenge will check that argv[NUM] holds value VALUE (listed to the right as NUM:VALUE) : 245:value2
- the challenge will check that env[KEY] holds value VALUE (listed to the right as KEY:VALUE) : 37:value1  
```
var=`env -i 245=value1 ... ... ... value2`
echo $var
```

## ex 72
- the challenge checks for a specific parent process : shellscript
- the challenge will check that input is redirected from a specific file path : file
- the challenge will check that it is running in a specific current working directory : /tmp/directory
``` 
cd /tmp/directory
var=`/challenge/level < file`
echo $var
```

## ex 73  
- the challenge checks for a specific parent process : shellscript
- the challenge will check that it is running in a specific current working directory : /tmp/yppaqz
- the challenge will check to make sure that the parent's parent CWD to be different than the challenge's CWD  
```
```
???

## ex 74
- the challenge checks for a specific parent process : python
- the challenge will check that argv[NUM] holds value VALUE (listed to the right as NUM:VALUE) : 29:value
```
import subprocess
p1 = subprocess.run(["/challenge/embryoio_level74", "a" x 28, "value"])
```

## ex 76
- the challenge checks for a specific parent process : python
- the challenge will check that the environment is empty (except LC_CTYPE, which is impossible to get rid of in some cases)
- the challenge will check that env[KEY] holds value VALUE (listed to the right as KEY:VALUE) : 69:value
```
import subprocess
p1 = subprocess.run(["/bin/env", "-i", "69=value","/challenge/level"])
```
## ex 77
- the challenge checks for a specific parent process : python
- the challenge will check that the environment is empty (except LC_CTYPE, which is impossible to get rid of in some cases)
- the challenge will check that argv[NUM] holds value VALUE (listed to the right as NUM:VALUE) : 262:value2
- the challenge will check that env[KEY] holds value VALUE (listed to the right as KEY:VALUE) : 311:value1
```
import subprocess
p1 = subprocess.run(["/bin/env", "-i", "311=value1", "/challenge/embryoio_level77", ... ... ... "value2"])
```

## ex 78
- the challenge checks for a specific parent process : python
- the challenge will check that input is redirected from a specific file path : file
- the challenge will check that it is running in a specific current working directory : /tmp/directory
```
import subprocess
i = open("file", "r")
subprocess.run(["/challenge/level"], stdin=i)
```

## ex 79
- the challenge checks for a specific parent process : python
- the challenge will check that it is running in a specific current working directory : /tmp/fxyjmt
- the challenge will check to make sure that the parent's parent CWD to be different than the challenge's CWD  
???

## ex 80
- the challenge checks for a specific parent process : binary
- the challenge will check that argv[NUM] holds value VALUE (listed to the right as NUM:VALUE) : 177:value  
same as 29 but:
```
for (int i = 1; i <= 178; i++)
  argv[i] = "value";
```

## ex 82
- the challenge checks for a specific parent process : binary
- the challenge will check that the environment is empty (except LC_CTYPE, which is impossible to get rid of in some cases)
- the challenge will check that env[KEY] holds value VALUE (listed to the right as KEY:VALUE) : 255:value
same as 29 but:  
```
char **argp = calloc(10, sizeof(char*));
...
argp[0] = "255=value";
execve(argv[0], (char **)argv, (char **)argp);
```

## ex 83
- the challenge checks for a specific parent process : binary
- the challenge will check that the environment is empty (except LC_CTYPE, which is impossible to get rid of in some cases)
- the challenge will check that argv[NUM] holds value VALUE (listed to the right as NUM:VALUE) : 103:value2
- the challenge will check that env[KEY] holds value VALUE (listed to the right as KEY:VALUE) : 133:value1
same as 29 but:  
```
char **argp = calloc(10, sizeof(char*));
...
for (int i = 1; i <= 103; i++)
  argv[i] = "value2";
argp[0] = "133=value1";
execve(argv[0], (char **)argv, (char **)argp);
```

## ex 84
- the challenge checks for a specific parent process : binary
- the challenge will check that input is redirected from a specific file path : file
- the challenge will check that it is running in a specific current working directory : /tmp/dir  
same as 29 but:
```
chdir("/tmp/dir");
int fd = open("/tmp/dir/file", O_RDONLY);
dup2(fd, 0);
```

## ex 85
- the challenge checks for a specific parent process : binary
- the challenge will check that it is running in a specific current working directory : /tmp/dir
- the challenge will check to make sure that the parent's parent CWD to be different than the challenge's CWD
same as 29 but:
```
chdir("/tmp/dir");
```

## ex 86
- the challenge checks for a specific parent process : shellscript
- the challenge will force the parent process to solve a number of arithmetic problems : 1
- the challenge will use the following arithmetic operations in its arithmetic problems : +*
- the complexity (in terms of nested expressions) of the arithmetic problems : 1  
just execute the challenge with shellscript

## ex 87
- the challenge checks for a specific parent process : shellscript
- the challenge will force the parent process to solve a number of arithmetic problems : 5
- the challenge will use the following arithmetic operations in its arithmetic problems : +*%
- the complexity (in terms of nested expressions) of the arithmetic problems : 3  
same as 86 but more annoying

## ex 88
- the challenge checks for a specific parent process : shellscript
- the challenge will check that argv[NUM] holds value VALUE (listed to the right as NUM:VALUE) : 0:/tmp/dir
```
var=`exec -a /tmp/dir /challenge/level`
echo $var
```

## ex 89
- the challenge checks for a specific parent process : shellscript
- the challenge will check that argv[NUM] holds value VALUE (listed to the right as NUM:VALUE) : 0:value  
same as 88

# ex 90
- the challenge checks for a specific parent process : shellscript
- the challenge will make sure that stdin is redirected from a fifo
- the challenge will check for a hardcoded password over stdin : password
```
mkfifo named_pipe
echo vdkohxym > named_pipe &
var=`/challenge/level < named_pipe`
echo $var
```

## ex 91
- the challenge checks for a specific parent process : shellscript
- the challenge will make sure that stdout is a redirected from fifo
```
var=`/challenge/level > named_pipe`
```

## ex 92
- the challenge checks for a specific parent process : shellscript
- the challenge will make sure that stdin is redirected from a fifo
- the challenge will make sure that stdout is a redirected from fifo
- the challenge will check for a hardcoded password over stdin : password
```
```  
???

## ex 93
- the challenge checks for a specific parent process : shellscript
- the challenge will make sure that stdin is redirected from a fifo
- the challenge will make sure that stdout is a redirected from fifo
- the challenge will force the parent process to solve a number of arithmetic problems : 1
- the challenge will use the following arithmetic operations in its arithmetic problems : +*
- the complexity (in terms of nested expressions) of the arithmetic problems : 1
```
```  
???

## ex 94
- the challenge checks for a specific parent process : shellscript
- the challenge will take input on a specific file descriptor : 70
- the challenge will check for a hardcoded password over stdin : password  
```
exec 70<> /tmp/foo
/challenge/embryoio_level94
exec 70>&-
```

## ex 95
- the challenge checks for a specific parent process : shellscript
- the challenge will take input on a specific file descriptor : 2
- the challenge will check for a hardcoded password over stdin : password  
just execute the challenge with shellscript

## ex 96
- the challenge checks for a specific parent process : shellscript
- the challenge will take input on a specific file descriptor : 1
- the challenge will check for a hardcoded password over stdin : password  
same as 95

## ex 97
- the challenge checks for a specific parent process : shellscript
- the challenge will require the parent to send number of signals : 1  
same as 95

## ex 98
- the challenge checks for a specific parent process : shellscript
- the challenge will require the parent to send number of signals : 5  
```
challenge="$1"
echo $challenge
if [ ! -z "$challenge" ]; then
    segnali=${challenge#*:}
    pid=${challenge%:*}
    pid=`echo $pid | tr -dc "0-9"`
    echo "PID: " $pid
    segnali=`echo $segnali | tr "',][" " "`
    echo $segnali
    for segnale in $segnali
    do
        echo "Segnale: " $segnale
        kill -$segnale $pid
        sleep 0.1
    done
fi
```

## ex 99
- the challenge checks for a specific parent process : python
- the challenge will force the parent process to solve a number of arithmetic problems : 1
- the challenge will use the following arithmetic operations in its arithmetic problems : +*
- the complexity (in terms of nested expressions) of the arithmetic problems : 1  
```
import subprocess
p1 = subprocess.run(["/challenge/level"])
```

## ex 100
- the challenge checks for a specific parent process : python
- the challenge will force the parent process to solve a number of arithmetic problems : 5
- the challenge will use the following arithmetic operations in its arithmetic problems : +*%
- the complexity (in terms of nested expressions) of the arithmetic problems : 3  
same as 99

## ex 101
- the challenge checks for a specific parent process : python
- the challenge will check that argv[NUM] holds value VALUE (listed to the right as NUM:VALUE) : 0:/tmp/dir  
???

## ex 102
- the challenge checks for a specific parent process : python
- the challenge will check that argv[NUM] holds value VALUE (listed to the right as NUM:VALUE) : 0:dir 
???

## es 103
- the challenge checks for a specific parent process : python
- the challenge will make sure that stdin is redirected from a fifo
- the challenge will check for a hardcoded password over stdin : password  
same as 116

## ex 104
- the challenge checks for a specific parent process : python
- the challenge will make sure that stdout is a redirected from fifo  
```
python pyscript.py > FIFOX | cat FIFOOUT
```

## ex 105
- the challenge checks for a specific parent process : python
- the challenge will make sure that stdin is redirected from a fifo
- the challenge will make sure that stdout is a redirected from fifo
- the challenge will check for a hardcoded password over stdin : password  
???

## ex 106
- the challenge checks for a specific parent process : python
- the challenge will make sure that stdin is redirected from a fifo
- the challenge will make sure that stdout is a redirected from fifo
- the challenge will force the parent process to solve a number of arithmetic problems : 1
- the challenge will use the following arithmetic operations in its arithmetic problems : +*
- the complexity (in terms of nested expressions) of the arithmetic problems : 1  
???

## ex 107
- the challenge checks for a specific parent process : python
- the challenge will take input on a specific file descriptor : 242
- the challenge will check for a hardcoded password over stdin : password  
???

## ex 108
- the challenge checks for a specific parent process : python
- the challenge will take input on a specific file descriptor : 2
- the challenge will check for a hardcoded password over stdin : password  
same as 99

## ex 109
- the challenge checks for a specific parent process : python
- the challenge will take input on a specific file descriptor : 1
- the challenge will check for a hardcoded password over stdin : password  
same as 99

## ex 110
- the challenge checks for a specific parent process : python
- the challenge will require the parent to send number of signals : 1  
same as 99

## ex 111
- the challenge checks for a specific parent process : python
- the challenge will require the parent to send number of signals : 5  
same as 98

## ex 112
- the challenge checks for a specific parent process : binary
- the challenge will force the parent process to solve a number of arithmetic problems : 1
- the challenge will use the following arithmetic operations in its arithmetic problems : +*
- the complexity (in terms of nested expressions) of the arithmetic problems : 1
same as 29

## ex 113
- the challenge checks for a specific parent process : binary
- the challenge will force the parent process to solve a number of arithmetic problems : 5
- the challenge will use the following arithmetic operations in its arithmetic problems : +*%
- the complexity (in terms of nested expressions) of the arithmetic problems : 3
same as 29 but more annoying

## ex 114
- the challenge checks for a specific parent process : binary
- the challenge will check that argv[NUM] holds value VALUE (listed to the right as NUM:VALUE) : 0:/tmp/dir  
same as 29 but:
```
argv[0] = "/tmp/dir";
execve("/challenge/level", (char **)argv, (char **)argp);
```

## ex 115
- the challenge checks for a specific parent process : binary
- the challenge will check that argv[NUM] holds value VALUE (listed to the right as NUM:VALUE) : 0:file  
same as 114

## ex 116
- the challenge checks for a specific parent process : binary
- the challenge will make sure that stdin is redirected from a fifo
- the challenge will check for a hardcoded password over stdin : password  
```
./es < FIFOIN
```
```
echo password > FIFOIN
```
```
cat > FIFOIN
```

## ex 117
- the challenge checks for a specific parent process : binary
- the challenge will make sure that stdout is a redirected from fifo  
```
cat > FIFOOUT
```
```
./es > FIFOOUT
```

## ex 118
- the challenge checks for a specific parent process : binary
- the challenge will make sure that stdin is redirected from a fifo
- the challenge will make sure that stdout is a redirected from fifo
- the challenge will check for a hardcoded password over stdin : password  
???

## ex 119
- the challenge checks for a specific parent process : binary
- the challenge will make sure that stdin is redirected from a fifo
- the challenge will make sure that stdout is a redirected from fifo
- the challenge will force the parent process to solve a number of arithmetic problems : 1
- the challenge will use the following arithmetic operations in its arithmetic problems : +*
- the complexity (in terms of nested expressions) of the arithmetic problems : 1
???

## ex 120
- the challenge checks for a specific parent process : binary
- the challenge will take input on a specific file descriptor : 126
- the challenge will check for a hardcoded password over stdin : password
same as 29 but:  
```
int fd = open ("/tmp/ciao", O_RDONLY); //open the file
dup2 (fd, 126); //and copy the file descriptor fd into the descriptor number 5
```

## ex 121
- the challenge checks for a specific parent process : binary
- the challenge will take input on a specific file descriptor : 2
- the challenge will check for a hardcoded password over stdin : password  
same as 29

## ex 122
- the challenge checks for a specific parent process : binary
- the challenge will take input on a specific file descriptor : 1
- the challenge will check for a hardcoded password over stdin : password  
same as 29

## ex 123
- the challenge checks for a specific parent process : binary
- the challenge will require the parent to send number of signals : 1  
same as 29

## ex 124
- the challenge checks for a specific parent process : binary
- the challenge will require the parent to send number of signals : 5
same as 29 + 98

## ex 125
- the challenge checks for a specific parent process : shellscript
- the challenge will force the parent process to solve a number of arithmetic problems : 50
- the challenge will use the following arithmetic operations in its arithmetic problems : +*&^%|
- the complexity (in terms of nested expressions) of the arithmetic problems : 5  
same as 126

## ex 126
- the challenge checks for a specific parent process : shellscript
- the challenge will force the parent process to solve a number of arithmetic problems : 500
- the challenge will use the following arithmetic operations in its arithmetic problems : +*&^%|
- the complexity (in terms of nested expressions) of the arithmetic problems : 10  
```
cat > FIFOIN
```
```
/challenge/level < FIFOIN > FIFOOUT
```
```
cd ./empty
challenge=`tail -1 ../FIFOOUT`
challenge=${challenge#*: }
echo "print($challenge)" | python > ../FIFOIN
```
```
for i in {1..500}; do (./mathscript2.sh; sleep 0.5); done
```

## ex 127
- the challenge checks for a specific parent process : shellscript
- the challenge will require the parent to send number of signals : 50  
same as 98

## ex 128
- the challenge checks for a specific parent process : shellscript
- the challenge will require the parent to send number of signals : 500  
same as 98

## ex 129
- the challenge checks for a specific parent process : shellscript
- the challenge checks for a specific process at the other end of stdin : cat
- the challenge checks for a specific process at the other end of stdout : cat
- the challenge will force the parent process to solve a number of arithmetic problems : 50
- the challenge will use the following arithmetic operations in its arithmetic problems : +*&^%|
- the complexity (in terms of nested expressions) of the arithmetic problems : 5  
same as 126

## ex 130
- the challenge checks for a specific parent process : python
- the challenge will force the parent process to solve a number of arithmetic problems : 50
- the challenge will use the following arithmetic operations in its arithmetic problems : +*&^%|
- the complexity (in terms of nested expressions) of the arithmetic problems : 5  
same as 126

## ex 131
- the challenge checks for a specific parent process : python
- the challenge will force the parent process to solve a number of arithmetic problems : 500
- the challenge will use the following arithmetic operations in its arithmetic problems : +*&^%|
- the complexity (in terms of nested expressions) of the arithmetic problems : 10  
same as 126

## ex 132
- the challenge checks for a specific parent process : python
- the challenge will require the parent to send number of signals : 50
same as 98

## ex 133
- the challenge checks for a specific parent process : python
- the challenge will require the parent to send number of signals : 500
same as 98

## ex 134
- the challenge checks for a specific parent process : python
- the challenge checks for a specific process at the other end of stdin : cat
- the challenge checks for a specific process at the other end of stdout : cat
- the challenge will force the parent process to solve a number of arithmetic problems : 50
- the challenge will use the following arithmetic operations in its arithmetic problems : +*&^%|
- the complexity (in terms of nested expressions) of the arithmetic problems : 5  
same as 126

## ex 135
- the challenge checks for a specific parent process : binary
- the challenge will force the parent process to solve a number of arithmetic problems : 50
- the challenge will use the following arithmetic operations in its arithmetic problems : +*&^%|
- the complexity (in terms of nested expressions) of the arithmetic problems : 5  
same as 126

## ex 136
- the challenge checks for a specific parent process : binary
- the challenge will force the parent process to solve a number of arithmetic problems : 500
- the challenge will use the following arithmetic operations in its arithmetic problems : +*&^%|
- the complexity (in terms of nested expressions) of the arithmetic problems : 10  
same as 126

## ex 137
- the challenge checks for a specific parent process : binary
- the challenge will require the parent to send number of signals : 50  
same as 98

## ex 138
- the challenge checks for a specific parent process : binary
- the challenge will require the parent to send number of signals : 500  
same as 98

## ex 139
- the challenge checks for a specific parent process : binary
- the challenge checks for a specific process at the other end of stdin : cat
- the challenge checks for a specific process at the other end of stdout : cat
- the challenge will force the parent process to solve a number of arithmetic problems : 50
- the challenge will use the following arithmetic operations in its arithmetic problems : +*&^%|
- the complexity (in terms of nested expressions) of the arithmetic problems : 5  
same as 126 but:  
```
cat FIFOIN | ./es | cat > FIFOOUT
```

## ex 140
- the challenge checks for a specific (network) client process : shellscript
- the challenge will listen for input on a TCP port : 1356
- the challenge will force the parent process to solve a number of arithmetic problems : 5
- the challenge will use the following arithmetic operations in its arithmetic problems : +*%
- the complexity (in terms of nested expressions) of the arithmetic problems : 3  
```
cd ./empty

exec 3<>/dev/tcp/127.0.0.1/1356

while read line <&3
do
    echo $line
    challenge=`echo $line | grep " Please send the solution for"`
    if [ ! -z "$challenge" ];
    then
        challenge=${challenge#*: }
        echo "Challenge: " $challenge
        echo "print($challenge)" | python >&3
    fi
done
```

## ex 141
- the challenge checks for a specific (network) client process : python
- the challenge will listen for input on a TCP port : 1927
- the challenge will force the parent process to solve a number of arithmetic problems : 5
- the challenge will use the following arithmetic operations in its arithmetic problems : +*%
- the complexity (in terms of nested expressions) of the arithmetic problems : 3  
???

## ex 142
- the challenge checks for a specific (network) client process : binary
- the challenge will listen for input on a TCP port : 1493
- the challenge will force the parent process to solve a number of arithmetic problems : 5
- the challenge will use the following arithmetic operations in its arithmetic problems : +*%
- the complexity (in terms of nested expressions) of the arithmetic problems : 3  
???