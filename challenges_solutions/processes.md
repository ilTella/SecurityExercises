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

# ex 31
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

# ex 34
same as 29

# ex 35
same as 29 but executed with
```
env --ignore-environment
```

# ex 36
- the challenge checks for a specific parent process : bash
- the challenge checks for a specific process at the other end of stdout : cat

```
/challenge/level | cat
```

# ex 37
- the challenge checks for a specific parent process : bash
- the challenge checks for a specific process at the other end of stdout : grep
```
/challenge/level | grep flag_prefix
```

# ex 38
- the challenge checks for a specific parent process : bash
- the challenge checks for a specific process at the other end of stdout : sed
???

# ex 39
- the challenge checks for a specific parent process : bash
- the challenge checks for a specific process at the other end of stdout : rev
```
/challenge/level | rev | rev
```

# ex 40
- the challenge checks for a specific parent process : bash
- the challenge checks for a specific process at the other end of stdin : cat
- the challenge will check for a hardcoded password over stdin : password
```
cat - | /challenge/level
```

# ex 41
- the challenge checks for a specific parent process : bash
- the challenge checks for a specific process at the other end of stdin : rev
- the challenge will check for a hardcoded password over stdin : password
```
rev | /challenge/level
```
then write the password reversed

# ex 42
- the challenge checks for a specific parent process : shellscript
- the challenge checks for a specific process at the other end of stdout : cat
```
#! /usr/bin/bash

var=`/challenge/level | cat`
echo $var
```

# ex 43
- the challenge checks for a specific parent process : shellscript
- the challenge checks for a specific process at the other end of stdout : grep
```
#! /usr/bin/bash

var=`/challenge/level | grep flag_prefix`
echo $var
```

# ex 44
- the challenge checks for a specific parent process : shellscript
- the challenge checks for a specific process at the other end of stdout : sed
???

# ex 45
- the challenge checks for a specific parent process : shellscript
- the challenge checks for a specific process at the other end of stdout : rev
```
#! /usr/bin/bash

var=`/challenge/level| rev | rev`
echo $var
```

# ex 46
- the challenge checks for a specific parent process : shellscript
- the challenge checks for a specific process at the other end of stdin : cat
- the challenge will check for a hardcoded password over stdin : password
```
#! /usr/bin/bash

var=`cat - | /challenge/level`
echo $var
```

# ex 47
- the challenge checks for a specific parent process : shellscript
- the challenge checks for a specific process at the other end of stdin : rev
- the challenge will check for a hardcoded password over stdin : password
```
#! /usr/bin/bash

var=`rev | /challenge/level`
echo $var
```

# ex 48
- the challenge checks for a specific parent process : ipython
- the challenge checks for a specific process at the other end of stdout : cat
```
ipython
import subprocess
p1 = subprocess.Popen(["/challenge/level"], stdout=subprocess.PIPE)
p2 = subprocess.run(["/bin/cat"], stdin=p1.stdout)
```

# ex 49
- the challenge checks for a specific parent process : ipython
- the challenge checks for a specific process at the other end of stdout : grep
```
ipython
import subprocess
p1 = subprocess.Popen(["/challenge/level"], stdout=subprocess.PIPE)
p2 = subprocess.run(["/bin/grep", "flag_prefix"], stdin=p1.stdout)
```

# ex 50
- the challenge checks for a specific parent process : ipython
- the challenge checks for a specific process at the other end of stdout : sed
???

# ex 51
- the challenge checks for a specific parent process : ipython
- the challenge checks for a specific process at the other end of stdout : rev
```
ipython
import subprocess
p1 = subprocess.Popen(["/challenge/level"], stdout=subprocess.PIPE)
p2 = subprocess.Popen(["/bin/rev"], stdin=p1.stdout, stdout=subprocess.PIPE)
p3 = subprocess.run(["/bin/rev"], stdin=p2.stdout)
```

# ex 52
- the challenge checks for a specific parent process : ipython
- the challenge checks for a specific process at the other end of stdin : cat
- the challenge will check for a hardcoded password over stdin : hybsgpbp
???