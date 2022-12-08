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
???

## ex 53
- the challenge checks for a specific parent process : ipython
- the challenge checks for a specific process at the other end of stdin : rev
- the challenge will check for a hardcoded password over stdin : password  
???

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
```
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/wait.h>

void pwncollege(void) {
  int pipefds[2];

  char **argv1 = calloc(5, sizeof(char*));
  argv1[0] = "/challenge/level";

  char **argv2 = calloc(5, sizeof(char*));
  argv2[0] = "/bin/cat";
 
  if (pipe(pipefds) == -1) {
    perror("pipe");
    exit(EXIT_FAILURE);
  }
 
  pid_t pid = fork();
 
  if (pid == 0) { // in child process
    close(pipefds[0]);
    dup2(pipefds[1], 1);
    execve(argv1[0], (char **)argv1, NULL); //***
  }
 
  if (pid > 0) { // in main process
    wait(NULL);
    dup2(pipefds[0], 0);
    close(pipefds[1]);
    execve(argv2[0], (char **)argv2, NULL); //***
  }
 
}

int main(void) {
    pwncollege();
    return 0;
}
```  
???

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
???

## ex 71
- the challenge checks for a specific parent process : shellscript
- the challenge will check that the environment is empty (except LC_CTYPE, which is impossible to get rid of in some cases)
- the challenge will check that argv[NUM] holds value VALUE (listed to the right as NUM:VALUE) : 245:value
- the challenge will check that env[KEY] holds value VALUE (listed to the right as KEY:VALUE) : 37:value   
???

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
???

## ex 74
- the challenge checks for a specific parent process : python
- the challenge will check that argv[NUM] holds value VALUE (listed to the right as NUM:VALUE) : 29:value
```
import subprocess
p1 = subprocess.run(["/challenge/embryoio_level74", "a" x 28, "value"])
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

## ex 80
- the challenge checks for a specific parent process : binary
- the challenge will check that argv[NUM] holds value VALUE (listed to the right as NUM:VALUE) : 177:value  
same as 29 but:
```
for (int i = 1; i <= 178; i++)
  argv[i] = "value";
```